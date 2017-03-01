### Python Unit testing framework
-- 3.6.0 버전 기준
#### 기본 개념
- test fixture
  - 테스트를 하기전 준비해야 할 것들
- test case
  - 각 개별적인 unit test
- test suite
  - collection of test cases
- test runner
  - test case를 실제로 수행하고 결과를 줌.

#### basic example

```python
  import unittest

class TestStringMethods(unittest.TestCase):

  def test_upper(self):
      self.assertEqual('foo'.upper(), 'FOO')

  def test_isupper(self):
      self.assertTrue('FOO'.isupper())
      self.assertFalse('Foo'.isupper())

  def test_split(self):
      s = 'hello world'
      self.assertEqual(s.split(), ['hello', 'world'])
      # check that s.split fails when the separator is not a string
      with self.assertRaises(TypeError):
          s.split(2)

if __name__ == '__main__':
  unittest.main()
```
- unittest.TestCase의 subclass
- test fixture 정의
  - def setUp(self) : 초기 셋팅
  - def tearDown(self) : 끝난 후 리소스 정리
- test suite 정의
  ```python
  def suite():
      suite = unittest.TestSuite()
      suite.addTest(someTesting())
      suite.addTest(someTesting1())
      return suite
  ```

#### Assert Method

  - assertEqual(a, b)
  - assertNotEqual(a, b)
  - assertTrue(x)
  - assertFalse(x)
  - assertIs(a, b)	a is b
  - assertIsNot(a, b)
  - assertIsNone(x)
  - assertIsNotNone(x)
  - assertIn(a, b)
  - assertNotIn(a, b)
  - assertIsInstance(a, b)
  - assertNotIsInstance(a, b)
  - assertRaises(exc, fun, *args, **kwds)
	 - fun(*args, **kwds) raises exception	 
  - assertRaisesRegex(exc, r, fun, *args, **kwds)
    -fun(*args, **kwds) raises exception and the message matches regex r
  - assertWarns(warn, fun, *args, **kwds)
    - fun(*args, **kwds) raises warn
  - assertWarnsRegex(warn, r, fun, *args, **kwds)
    - fun(*args, **kwds) raises warn and the message matches regex r
  - assertLogs(logger, level)
    - logger = Logger object or logger name
    ```python
      with self.assertLogs('foo', level='INFO') as cm:
        # execution test example
       logging.getLogger('foo').info('first message')
       logging.getLogger('foo.bar').error('second message')
      self.assertEqual(cm.output, ['INFO:foo:first message',
                           'ERROR:foo.bar:second message'])
    ```
    - 결과 = string list
  - 추가 정보 https://docs.python.org/3/library/unittest.html#test-cases

#### skipping test, expected failures

- 테스트 건너 뛰기
  - @unittest.skip(reason)
  - @unittest.skipIf(condition, reason)
  - @unittest.skipUnless(condition, reason)
  - exception unittest.SkipTest(reason)
- 실패를 예측하기
  - @unittest.expectedFailure
