---
layout:              post
title:                  "Hello test"
subtitle:            " \"Hello TEST,\""
date:                 2019-01-02 11:08:00 +0800
author:             "SNLO"
header-img:     "img/post-bg-apple-event-2015.jpg"
catalog:            true
tags:
- 生活
---
## 正文

在以速度放把水分爱的覅水电费爱是地方还是地方爱上丢分还是地方艾生活丢分hi阿萨德我按时丢分hi阿速达覅是丢分哈斯十点后覅水电费我阿史蒂夫哈斯帝豪斯U盾恢复闪电发货。

#### 家家爱建设大街将发送

拉卡萨诺的开发商

asndnfasn dfinasidfnipasndfijnasidjn fijansidjnfjansdijfnjasndfnjiasn djnfiajsndjfne wjnifnqwe uqewirquweoruq woeuroq wueofji wejfiqwj efijqweiofobjectivec

```objectivec
- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {
    switch (indexPath.row) {
        case 0: {
            DecorationCompanyMonthCell * cell = [DecorationCompanyMonthCell sn_nibCellWithTabelView:tableView indexPath:indexPath];
            cell.selectionStyle = UITableViewCellSelectionStyleNone;
            cell.labelOrderNum.text = self.viewmodelAccountSystem.modelPersonalCore.monthOrder?:@"0";
            cell.labelAmount.text = SNString(@"￥%@",self.viewmodelAccountSystem.modelPersonalCore.monthIncome?:@"0.00");
            return cell;
        } break;
        case 1: { //余额
            DecorationCompanyBalanceCell * cell = [DecorationCompanyBalanceCell sn_nibCellWithTabelView:tableView indexPath:indexPath];
            cell.selectionStyle = UITableViewCellSelectionStyleNone;
            cell.labelBlance.text = self.viewmodelAccountSystem.modelPersonalCore.money?:@"0.00";
            [[[cell.buttonSelected rac_signalForControlEvents:UIControlEventTouchUpInside] takeUntil:cell.rac_prepareForReuseSignal] subscribeNext:^(__kindof UIControl * _Nullable x) {
#pragma mark -- 余额
                UIViewController * VC = [[SNMediator sharedManager] SNMediator_viewControllerForBalanceBase:@{@"availableamount":self.viewmodelAccountSystem.modelPersonalCore.money}];
                [self.navigationController pushViewController:VC animated:YES];
            }];
            return cell;
        } break;
        case 2: { //功能菜单
            DecorationCompanyWaresControlCell * cell = [DecorationCompanyWaresControlCell sn_nibCellWithTabelView:tableView indexPath:indexPath];
            cell.selectionStyle = UITableViewCellSelectionStyleNone;
            @weakify(self);
            [[cell.subjectButton takeUntil:cell.rac_prepareForReuseSignal] subscribeNext:^(id  _Nullable x) {
                NSDictionary * dic = x;
                UIButton * button = dic.allValues.firstObject;
                NSIndexPath * indexPath = dic.allKeys.firstObject;
                @strongify(self);
                [self handleBusinessMallControlMenuEvent:button indexPath:indexPath];
            }];
            self.cellWares = cell;
            return cell;
        } break;
        default: {
            return [UITableViewCell new];
        } break;
    }
}

```



##### 后记

阿斯蒂芬阿萨德你过分，爱三点半覅是。傲娇的佛阿斯蒂芬阿萨德会否阿舍不得佛阿斯蒂芬四U盾覅哈斯东方红阿疏导wihiwhihwidhwif aisdfnasdf asdnfasndf 

