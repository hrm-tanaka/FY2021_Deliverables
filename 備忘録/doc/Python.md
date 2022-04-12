

#### pythonのバージョン登録・管理
* 登録されているpythonのバージョンや優先順位を見る
```
$ sudo update-alternatives --config python
update-alternatives: error: no alternatives for python    #まだpythonが登録されていない状態です
```

```
$ update-alternatives --config python
There are 2 choices for the alternative python (providing /usr/bin/python).

  Selection    Path                Priority   Status
------------------------------------------------------------
  0            /usr/bin/python2.7   2         auto mode
* 1            /usr/bin/python2.7   2         manual mode
  2            /usr/bin/python3.6   1         manual mode
Press <enter> to keep the current choice[*], or type selection number: 2    #python3.6を使用したいのでSelectionの2を入力
update-alternatives: using /usr/bin/python3.6 to provide /usr/bin/python (python) in manual mode
```
