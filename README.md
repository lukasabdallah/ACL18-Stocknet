# ACL18-Stocknet

For an initial comparison following metrics are used:
- Accuracy
- Matthews Correlation Coefficient (MCC): avoids bias due to data skew and assures that predictions are balanced over classes

For a more detailed comparison with the top baselines I used additional metrics following the STLAT paper:
- Specificity ( recall of negative class )
- Precision
- Sensitivity ( recall of positive class )
- F1- score

In the end I provided the confusion matrices of the proposed models

STLAT (2022) states: the best two baselines on the ACL18 (Stocknet) Datasetset are Adv-ALSTM and MAN-SF.

I decided between the Stocknet and Adv-ALSTM approach as those two have working implementations and decent scores.
I chose the Adv-ALSTM (https://github.com/fulifeng/Adv-ALSTM) in the end, because it has more balanced predictions (better MCC scores) than Stocknet, that I think are worth the tradeoff in accuracy. 

I trained two models denoted as:
- **Adv-ALSTM_val**: the one performing best on the val set
- **Adv-ALSTM_test**: the one performing best on the test set


If opting for the absolute best scores, I think the way would be to reproduce the STLAT approach first. This approach doesn't use tweets so it could be enhanced by for example including the Market Information Encoder (MIE) of the Stocknet approach (Figure 2 in the Stocknet paper) or some other form of social information encoding shown in the other papers.



## Table 1: Overview of approaches
|   Model               | Year |   Using tweets  |   Accuracy    |   MCC         | Paper                                                             | Implementation                                                                                              |
|-----------------------|------|-----------------|---------------|---------------|-------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|
|   Stocknet_technical  | 2018 |   No            |   0.55        |   0.017       | https://aclanthology.org/P18-1183.pdf                             | https://github.com/yumoxu/stocknet-code                                                                     |
|   Adv-ALSTM_org            | 2019 |   No            |   0.572       |   0.148       | https://www.ijcai.org/proceedings/2019/0810.pdf               | https://github.com/fulifeng/Adv-ALSTM                                                                       |
| **Adv-ALSTM_val**                  | - |   No            |   0.5712      |   0.1433      | -            | -                                                                                                           |
| **Adv-ALSTM_test**                  | - |   No            |   0.5833      |   0.1666      | -            | -                                                                                                           |
| DTML                  | 2021 |   No            |   0.5812      |   0.1806      | https://datalab.snu.ac.kr/~ukang/papers/dtmlKDD21.pdf             | -                                                                                                           |
|   SLOT                | 2022 | Yes             |   0.5872      |   0.2065      | https://jaeminyoo.github.io/resources/papers/SounYCJK22.pdf       | -                                                                                                           |
|   StockNet            | 2018 |   Yes           |   0.582       |   0.081       | https://aclanthology.org/P18-1183.pdf                             | https://github.com/yumoxu/stocknet-code                                                                     |
|   MAN-SF              | 2020 |   Yes           |   0.608       |   0.195       | https://aclanthology.org/2020.emnlp-main.676.pdf                  | Repo has some issues  https://github.com/midas-research/man-sf-emnlp  |
|   STLAT               | 2022 |   No            | **0.6456** | **0.2967** | https://www.tandfonline.com/doi/pdf/10.1080/09540091.2021.2021143 | -                                                                                                           |

## Table 2: Further comparison with strongest approaches 
|   Model        | Specificity(%) |   Precision(%) |   Sensitivity (%) |   F1-Score (%) |
|----------------|----------------|----------------|-------------------|------------|
| Adv-ALSTM_val      | 59             |   59           |   56              |   57       |
| Adv-ALSTM_test | 58             | 60             | 58                | 59         |
|   MAN-SF       | 58.11          |   61.44        |   58.16           |   59.75    |
| STLAT     | **63.14**          |   **65.15**        |   **63.19**           |   **64.15**   |


Confusion matrices with form:
|   TN | FP  |
|--------|------|
| FN    | TP |

Adv-ALSTM_val:
|   1065 | 747  |
|--------|------|
| 848    |1060 |

Adv-ALSTM_test:
|   1055 | 757  |
|--------|------|
| 793    | 1115 |
