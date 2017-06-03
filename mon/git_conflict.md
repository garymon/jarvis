Git conflict
-------
- 처음에 git붙인후, 첫 commit후 push하려 하였지만 충돌이 일어나서 되지 않는 상황. 여기서 pull후 다시 push 하라는 메세지를 본후 pull하려 하였으나 아래 메시지와 함께 되지 않음


 * git pull에서 충돌 날떄 대응,,

~~~~~~
Junui-MacBook-Pro:perikles.github.io jun$ git pull origin master
From https://github.com/SeoHyeokJun/perikles.github.io
 * branch            master     -> FETCH_HEAD
fatal: refusing to merge unrelated histories
~~~~~~

 * 아래 옵션을 추가해서 pull 시도~!!

~~~~~~
git pull origin master --allow-unrelated-histories
~~~~~~


 * error가 났던 이유는

~~~~~
"git merge" used to allow merging two branches that have no common base by default, which led to a brand new history of an existing project created and then get pulled by an unsuspecting maintainer, which allowed an unnecessary parallel history merged into the existing project. The command has been taught not to allow this by default, with an escape hatch "--allow-unrelated-histories" option to be used in a rare event that merges histories of two projects that started their lives independently.
~~~~~
