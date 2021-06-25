---
layout:     post
title:      "pytest退出码"
subtitle:   ""
date:       2021-06-25
author:     "Tesla9527"
header-img: "img/vancleefarpels.jpg"
tags:
    - pytest
---

pytest的退出码有如下6种

```
OK = 0
Tests passed.

TESTS_FAILED = 1
Tests failed.

INTERRUPTED = 2
pytest was interrupted.

INTERNAL_ERROR = 3
An internal error got in the way.

USAGE_ERROR = 4
pytest was misused.

NO_TESTS_COLLECTED = 5
pytest couldn’t find tests.
```

我们可以通过这个退出码，来判定执行是否成功。下面这段脚本，是判定如果退出码不为0，就执行异常退出。

```python
# -*- coding: utf-8 -*-
import os
import time
import argparse
import pytest
import sys



def run(args):
    """
    执行用例并生成allure报告，pycharm执行会报提示allure不是内部命令，windows在cmd执行，Mac在终端执行
    :param testcases:
    :return:
    """
    testcases = args.testcases
    report_path = args.reportpath or 'report/{}'.format(time.strftime("%Y%m%d"))
    if not os.path.exists(report_path):
        os.makedirs(report_path)
    args_list = [f'--alluredir={report_path}/data']
    for testcase in testcases.split(','):
        args_list.insert(0, testcase)
    args_list.insert(0, '-s')
    exit_code = pytest.main(args=args_list)
    os.system(f'allure generate {report_path}/data -o {report_path}/html --clean')
    print(exit_code)
    if exit_code.value == 0:
        print('用例执行成功!')
    else:
        sys.exit(f"执行出现异常: {exit_code.name}")



if __name__ == '__main__':
    parser = argparse.ArgumentParser(usage="it's usage tip.", description="help info.")
    # parser.add_argument("--domain", type=str, required=True)
    parser.add_argument("--testcases", type=str, required=True)
    parser.add_argument("--reportpath", type=str)
    args = parser.parse_args()
    run(args)
```

该种方式时，在Jenkins中可以这样配置

```shell
python run.py --testcases ${testcases} --reportpath ${WORKSPACE}/result/${BUILD_ID}
```

使用Allure插件构建后的操作,Path进行如下配置

```
result/${BUILD_ID}/data
```

下面这段代码，是判定如果退出码不为0，不执行异常退出，而是打印成功与否的标识。这样的shell脚本中执行的时候，可以有办法获取到这个成功与否的标识。比如在Jenkins中执行时，获取到这个后，就能够更精确的控制执行结果。

```python
# -*- coding: utf-8 -*-
import os
import time
import argparse
import pytest
import sys



def run(args):
    """
    执行用例并生成allure报告，pycharm执行会报提示allure不是内部命令，windows在cmd执行，Mac在终端执行
    :param testcases:
    :return:
    """
    testcases = args.testcases
    report_path = args.reportpath or 'report/{}'.format(time.strftime("%Y%m%d"))
    if not os.path.exists(report_path):
        os.makedirs(report_path)
    args_list = [f'--alluredir={report_path}/data']
    for testcase in testcases.split(','):
        args_list.insert(0, testcase)
    args_list.insert(0, '-s')
    exit_code = pytest.main(args=args_list)
    os.system(f'allure generate {report_path}/data -o {report_path}/html --clean')
    print(exit_code)
    if exit_code.value == 0:
        print('\nsuccess')
    else:
        print('\nfail')



if __name__ == '__main__':
    parser = argparse.ArgumentParser(usage="it's usage tip.", description="help info.")
    # parser.add_argument("--domain", type=str, required=True)
    parser.add_argument("--testcases", type=str, required=True)
    parser.add_argument("--reportpath", type=str)
    args = parser.parse_args()
    run(args)
```


该种方式时，在Jenkins中可以这样配置

```shell
# 用例执行结果标识
flag=0

output=$(python run.py --testcases ${testcases}/attach --reportpath ${WORKSPACE}/result/${BUILD_ID})
# 读取输出内容中的最后一行，也就是上面脚本中打印出来的success或fail
result="${output##*$'\n'}"
if [[ $result == "success" ]];
then
    echo "用例执行成功"
else
    echo "用例执行失败"
    flag=$((flag+1))
fi

#########分割线#########
echo $flag
if (( $flag == 0 ));
then
    echo "所有用例执行成功"
else
    echo "执行存在错误"
    exit 1
fi
```

使用Allure插件构建后的操作,Path进行如下配置

```
result/${BUILD_ID}/data
```
