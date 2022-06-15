 红色 榴弹144

·

```
//M200-幻神
//王者涂鸦
//觉醒版王者之锋
//觉醒版王者之灵
//屠龙
//加特林-炼狱
//Barret-朱雀
//沙鹰-天神
//炫金千变
;//A背包套装-手雷包
;//100积分
;//50积分
;//20积分
;//10积分
/5积分
0.002;
0.004;
0.009;
0.016;
0.045;
0.065;
0.085;
0.100;
0.120;
 0.180
 0.190
 0.220
 0.450
 0.750
 0.1;/
```

|          | 榴弹 | 群伤 | 单体 | 技能 |
| :------: | ---- | :--- | ---- | ---- |
| 暴君乱世 |      |      | 最高 | 2/3  |
| 火狱乱世 | 144  |      | 低   |      |
| 致命乱世 |      |      | 中   |      |
|          |      |      |      |      |

|                  | 中奖概率 |      |
| ---------------- | -------- | ---- |
| M200-幻神        | 0.1%     |      |
| 王者涂鸦         | 0.2%     |      |
| 觉醒版王者之锋   | 0.5%     |      |
| 觉醒版王者之灵   | 0.7%     |      |
| 屠龙             | 2.9%     |      |
| 加特林-炼狱      | 2%       |      |
| Barret-朱雀      | 2%       |      |
| 沙鹰-天神        | 1.5%     |      |
| 炫金千变         | 1%       |      |
| A背包套装-手雷包 | 6%       |      |
| 100积分          | 3%       |      |
| 50积分           | 23%      |      |
| 20积分           | 30%      |      |
| 5积分            | 25%      |      |

```java
package com.webex.gfc;

import java.text.DecimalFormat;
import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.ThreadLocalRandom;

public class Game {

    double ran1 = 0.002;//M200-幻神
    double ran2 = 0.004;//王者涂鸦
    double ran3 = 0.009;//觉醒版王者之锋
    double ran4 = 0.016;//觉醒版王者之灵
    double ran5 = 0.045;//屠龙
    double ran6 = 0.065;//加特林-炼狱
    double ran7 = 0.085;//Barret-朱雀
    double ran8 = 0.100;//沙鹰-天神
    double ran9 = 0.120;//炫金千变
    double ran10 = 0.180;//A背包套装-手雷包
    double ran11 = 0.190;//100积分
    double ran12 = 0.220;//50积分
    double ran13 = 0.350;//20积分
    double ran14 = 0.450;//10积分
    double ran15 = 0.659;//5积分
    double ran16 = 0.999;//5积分


    public String result() throws Exception {
        DecimalFormat df = new DecimalFormat("#.00000");
        double random = ThreadLocalRandom.current().nextDouble(0.0001, 0.9999);

        if (random < ran1 && random >= 0.0001){
            return "M200-幻神";
        }
        if (random < ran2 && random >= ran1){
            return "王者涂鸦";
        }
        if (random < ran3 && random >= ran2){
            return "觉醒版王者之锋";
        }
        if (random < ran4 && random >= ran3){
            return "觉醒版王者之灵";
        }
        if (random < ran5 && random >= ran4){
            return "屠龙";
        }
        if (random < ran6 && random >= ran5){
            return "加特林-炼狱";
        }
        if (random < ran7 && random >= ran6){
            return "Barret-朱雀";
        }
        if (random < ran8 && random >= ran7){
            return "沙鹰-天神";
        }
        if (random < ran9 && random >= ran8){
            return "炫金千变";
        }
        if (random < ran10 && random >= ran9){
            return "A背包套装-手雷包";
        }
        if (random < ran11 && random >= ran10){
            return "王者之石";
        }
        if (random < ran12 && random >= ran11){
            return "100积分";
        }
        if (random < ran13 && random >= ran12){
            return "50积分";
        }
        if (random < ran14 && random >= ran13){
            return "20积分";
        }
        if (random < ran15 && random >= ran14){
            return "10积分";
        }
        if (random < ran16 && random >= ran15){
            return "5积分";
        } else {
            return "5积分";
        }
    }


    public static void main(String[] args) throws Exception {
        Game g = new Game();
        List<List<String>> col = new ArrayList<>();

        System.out.println("幻神夺宝-10连抽");
        System.out.println("\t");
        for (int i = 0; i < 10; i++) {
            List<String> row = new ArrayList<>();
            for (int j = 0; j < 10; j++) {
                row.add(g.result());
            }
            col.add(i,row);
        }
        for (List<String> s: col) {
            System.out.println(s);
        }

    }

}

```

