---
layout:     post
title:      "使用python+selenium+pytest+allure做web自动化测试"
subtitle:   ""
date:       2020-04-09
author:     "Tesla9527"
header-img: "img/vancleefarpels.jpg"
catalog:    false
tags:
    - python
    - selenium
    - pytest
    - allure
---

## 目的
之前使用过C#，Java做过自动化测试，由于在测试技术领域，python几乎可以通吃，所以想把测试技术栈都移到python。在看过不少资料后，决定自己把框架重新搭建一下，期望达到换一个项目也能直接使用，只需要针对不同的测试页面写测试脚本即可。

## 框架的目录结构

![img](/img/in-post/webauto/framework.png)

## browser_engine.py
```python
from selenium import webdriver


class BrowserEngine(object):
    chrome_driver_path = '../driver/chromedriver.exe'

    def __init__(self, selenium_driver):
        self.driver = selenium_driver

    def get_driver(self):
        selenium_driver = webdriver.Chrome(self.chrome_driver_path)
        selenium_driver.maximize_window()
        selenium_driver.implicitly_wait(10)
        return selenium_driver
```

## base_page.py
```python
from .browser_engine import BrowserEngine
from selenium.webdriver.support.wait import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC


# 需要二次封装的方法都写在这里
class BasePage:
    chrome_driver_path = '../driver/chromedriver.exe'

    def __init__(self, selenium_driver):
        self.driver = selenium_driver
        # 上面的driver是当参数传入的,因为没有变量声明,所以driver的方法不能自动获取,会比较麻烦,所以在写当前page
        # 的操作方法时,可以把上面一句注释掉,下面一句打开,写完之后再恢复。
        # self.driver = BrowserEngine.get_driver()

    # *loc任意数量的位置参数（带单个星号参数）
    def find_element(self, *loc):
        try:
            WebDriverWait(self.driver, 10).until(EC.visibility_of_element_located(loc))
            return self.driver.find_element(*loc)
        except:
            print("%s 页面未能找到 %s 元素" % (self, loc))
```

## baidu_homepage.py
```python
import time
from po.base_page import BasePage
from selenium.webdriver.common.by import By
import allure


class BaiduHomePage(BasePage):
    # 个人感觉不太喜欢把页面元素，和操作脚本再单独分开，因为读起来累。
    search_box_loc = (By.ID, "kw")
    search_button_loc = (By.ID, "su")

    @allure.step('打开百度首页')
    def open_homepage(self):
        self.driver.get('https://www.baidu.com/')

    @allure.step('输入内容进行搜索')
    def search(self, search_char):
        search_box = self.find_element(*self.search_box_loc)
        search_box.send_keys(search_char)
        search_button = self.find_element(*self.search_button_loc)
        search_button.click()
        time.sleep(3)

    @allure.step('验证标题是否正确')
    def verify(self, verify_char):
        title = self.driver.title
        print(title)
        assert verify_char == title


```

## test_baidu_search.py
```python
import sys
sys.path.append("..")
from po.browser_engine import BrowserEngine
from po.baidu_homepage import BaiduHomePage
import pytest
import allure


@allure.feature("百度搜索")
class TestBaiduSearch:
    @classmethod
    def setup_class(cls):
        browse = BrowserEngine(cls)
        cls.driver = browse.get_driver()

    @classmethod
    def teardown_class(cls):
        cls.driver.quit()

    @allure.story("测试百度搜索，验证标题是否正确")
    @pytest.mark.parametrize("search_char, verify_char", [('龙珠', '龙珠_百度搜索'), ('火影忍者', '火影_百度搜索')])
    def test_baidu_search(self, search_char, verify_char):
        baidu_homepage = BaiduHomePage(self.driver)
        baidu_homepage.open_homepage()
        baidu_homepage.search(search_char)
        baidu_homepage.verify(verify_char)


if __name__ == '__main__':
    pytest.main()
```

## conftest.py
```python
import pytest
import allure
from allure_commons.types import AttachmentType
from PIL import ImageGrab
from io import BytesIO


# 钩子，用来钩住失败
@pytest.hookimpl(tryfirst=True, hookwrapper=True)
def pytest_runtest_makereport():
    outcome = yield
    rep = outcome.get_result()
    # we only look at actual failing test calls, not setup/teardown
    if rep.when == "call" and rep.failed:
        with BytesIO() as output:
            img = ImageGrab.grab()
            img.save(output, 'PNG')
            data = output.getvalue()
        # 将异常截图附加到allure报告中
        allure.attach(data, name="异常截图", attachment_type=AttachmentType.PNG)
```
