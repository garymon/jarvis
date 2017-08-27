### OAuth

* 인증을 위한 오픈 스탠다드 프로토콜

### OAuth with python

* google api client 설치

```
pip install oauth2client
pip install google-api-python-client # for build google service (profile, drive, etc...)

```
### Flow

* google login url로 redirect한다 (with callback url, client id)
  * flow.step1_get_authorize_url
* callback url로 들어온 request로 부터 ?code={code}를 얻은후 credentials을 얻는다
  * flow.step2_exchange
* credentials을 session에 저장하고 해당 credentials로 모든 google service에 접근하여 필요 데이터를 얻는다
  * discovery.build

### Full example
```python
from flask import Flask, redirect, url_for, request, render_template, send_from_directory, session
from oauth2client import clien
from apiclient import discovery
import httplib2

@app.route('/login')
def login():
    if 'user_info' not in session:
        return render_template("login.html")
    else:
        return redirect(url_for('index'))

@app.route('/oauth2/google')
def loginWithGoogle():
    if 'credentials' not in session:
        return redirect(url_for('oauth_callback'))
    credentials = client.OAuth2Credentials.from_json(session['credentials'])
    if credentials.access_token_expired:
        return redirect(url_for('oauth_callback'))
    else:
        user_info_service = discovery.build(
            serviceName='oauth2', version='v2',
            http=credentials.authorize(httplib2.Http()))
        user_info = None
        try:
            user_info = user_info_service.userinfo().get().execute()
            session['user_info'] = user_info
            session.modified = True
        except Exception as e:
            print('An error occurred: {0}'.format(str(e)))
        return redirect(url_for('index'))

@app.route('/logout')
def logout():
    if 'user_info' not in session:
        return redirect(url_for('index'))
    session.clear()
    return redirect(url_for('index'))


@app.route('/oauth2/google/callback')
def oauth_callback():
    flow = client.flow_from_clientsecrets('client_secrets.json',
                                          scope='https://www.googleapis.com/auth/userinfo.profile',
                                          redirect_uri=url_for('oauth_callback', _external=True))
    if 'code' not in request.args:
        auth_uri = flow.step1_get_authorize_url()
        return redirect(auth_uri)
    else:
        auth_code = request.args.get('code')
        credentials = flow.step2_exchange(auth_code)
        session['credentials'] = credentials.to_json()
        return redirect(url_for('loginWithGoogle'))

```

* client_secrets.json

```json
{
  "web": {
    "client_id": "client_id",
    "client_secret": "client_secret",
    "redirect_uris": ["http://localhost:18080/oauth2/callback"],
    "auth_uri": "https://accounts.google.com/o/oauth2/auth",
    "token_uri": "https://accounts.google.com/o/oauth2/token"
  }
}

```
