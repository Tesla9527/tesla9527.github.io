---
layout:     post
title:      "python替换字符串中特定string的值"
subtitle:   ""
date:       2018-04-19
author:     "Tesla9527"
header-img: "img/post-bg-alitrip.jpg"
tags:
    - python
---
>在工作中遇到一种需求，需要将一个csv文件中的各个key的值替换到json中的对应的值，写好脚本后运行也正常。但是觉得还可以继续优化，今天使用了一个for循环，使得脚本简练了不少。

```python
import csv


def write_dict_to_csv(csv_file, csv_columns, dict_data):
    try:
        with open(csv_file, 'w') as csvfile:
            writer = csv.DictWriter(csvfile, fieldnames=csv_columns, delimiter=',', lineterminator='\n')
            writer.writeheader()
            for data in dict_data:
                writer.writerow(data)
    except IOError as strerror:
        print("I/O error({0})".format(strerror))
    return

csv_file = r"D:\Tesla\xiaomi\input\xm_json.csv"

original_json = """{"ratings_user_general_score":"value101","ratings_user_mi_consume_score":"value102","ratings_user_credit_history_score":"value103","ratings_user_finance_interest_score":"value104","ratings_user_loan_interest_score":"value105","ratings_user_fund_interest_score":"value106","ratings_user_bank_interest_score":"value107","ratings_user_social_interest_score":"value108","ratings_user_shopping_interest_score":"value109","ratings_user_travel_interest_score":"value110","ratings_user_food_interest_score":"value111","ratings_user_game_interest_score":"value112","ratings_user_smartdevice_interest_score":"value113","ratings_finance_app_install_index":"value114","ratings_loan_app_install_index":"value115","ratings_fund_app_install_index":"value116","ratings_bank_app_install_index":"value117","ratings_social_app_install_index":"value118","ratings_shopping_app_install_index":"value119","ratings_travel_app_install_index":"value120","ratings_food_app_install_index":"value121","ratings_game_app_install_index":"value122","behavior_consumer_pay_sence_m12_model":"value123","behavior_consumer_book_money_m12_model":"value124","behavior_consumer_book_count_m12_model":"value125","behavior_consumer_mi_mall_money_m12_model":"value126","behavior_consumer_mi_mall_count_m12_model":"value127","credit_overdue_money_m1_model":"value128","credit_overdue_money_m3_model":"value129","credit_overdue_money_m6_model":"value130","credit_overdue_money_m12_model":"value131","credit_overdue_count_m1_model":"value132","credit_overdue_count_m3_model":"value133","credit_overdue_count_m6_model":"value134","credit_overdue_count_m12_model":"value135","credit_repay_money_m1_model":"value136","credit_repay_money_m3_model":"value137","credit_repay_money_m6_model":"value138","credit_repay_money_m12_model":"value139","credit_repay_count_m1_model":"value140","credit_repay_count_m3_model":"value141","credit_repay_count_m6_model":"value142","credit_repay_count_m12_model":"value143"}"""
result = []
with open(csv_file, encoding='utf-8') as csvfile:
    reader = csv.DictReader(csvfile)
    for row in reader:
        result_json = original_json
        count = 101
        for key in row:
            result_json = result_json.replace('value' + str(count), row[key])
            count += 1      
        print('result_json: ' + result_json)
        print('-----------------------------')
        result.append({'json': result_json})

csv_columns = ['json']
output_csv_file = r"D:\Tesla\xiaomi\output\xiaomi_result_json.csv"
write_dict_to_csv(output_csv_file, csv_columns, result)
```

要替换的值我们先在original_json中写死。第一个要替换的值为啥从value101开始呢？因为如果从value1开始的话，后面可能又value11,value12...之类的值，替换value1的时候可能把value11,value12...也替换掉了，这样容易造成混乱。从value101开始的话，至少一直到value999也不会有覆盖的情况，而且从value101到value999也有899个值了，一般情况是够用了的。