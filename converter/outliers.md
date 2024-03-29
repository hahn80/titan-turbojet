# THIS IS OUTLIER SERVICE WITH LEVELS

Note that, we need to run outlier as `converter` service to get the output as JSON format.

## Outlier (IQR)
Here is a sample json params:
```json
{
    "input": "outlier.arrow",
    "output": "output.json",
    "operations": [
    {
        "operator": "select",
        "options":
        {
            "columns": ["x1", "x2", "x3"]
        }
    },
    {
        "operator": "outlier_level",
        "options":
        {
            "outlier_name": "iqr",
            "columns": ["x2", "x3"],
            "key": "x1",
            "iqr_levels": [0.8, 1.3, 1.7],
            "metrics": ["q1", "q3", "count", "mean"]
        }
    }]
}
```
**Chú thích:**

- *outlier_name* has the following options:
  * iqr: Outlier using IQR
  * z_scores: Outlier using Z-Scores.
- *columns*: List of columns to check outliers.
- Kiểu dữ liệu cho columns là numerical (int, float).
- *key*: Kiểu dữ liệu string hoac int, float.
- `iqr_levels`: List of quartiles multiples (float type).
- `metrics`: support any of these ["mean", "median", "max", "min", "count", "q1", "q3"]


## Outlier (Z Scores)
Here is a sample json params:
```json
{
    "input": "outlier.arrow",
    "output": "output.json",
    "operations": [
    {
        "operator": "select",
        "options":
        {
            "columns": ["x1", "x2", "x3"]
        }
    },
    {
        "operator": "outlier_level",
        "options":
        {
            "outlier_name": "z_scores",
            "columns": ["x2", "x3"],
            "key": "x1",
            "z_levels": [1.75, 2.05, 2.7],
            "metrics": ["q1", "q3", "count", "mean"]
        }
    }]
}
```
**Chú thích:**
- `z_levels`: A list of 3 increasing float numbers. First number from 1.0 to 2.5; Second number from the first one to 3.0, the last value from the second one to 6.0
- The default values could be [1.75, 2.05, 2.7]



**Cách hiển thị kết quả:**

Chú ý: Outliers được chia ra các cấp độ khác nhau:
- `L1`: Ngoại biên cấp 1 (thấp)
- `L2`: Ngoại biên cấp 2 (thấp) -> moderate outliers
- `L3`: Ngoại biên cấp 3 (thấp) -> extreme outliers
- `H1`: Ngoại biên cấp 1 (cao)
- `H2`: Ngoại biên cấp 2 (cao) -> moderate outliers
- `H3`: Ngoại biên cấp 3 (cao) -> extreme outliers

```JSON
[
    {
        "key": "x1",
        "variable": "x2",
        "metrics": {
            "x2__q1": 0.08396551008680517,
            "x2__q3": 0.005947503078542492,
            "x2__count": 2.779788837189692,
            "x2__mean": -2.663488408212937
        },
        "outliers": {
            "L1": [
                {
                    "x1": 0.11307257833784189,
                    "x2": -2.1412915363007823
                },
                {
                    "x1": 0.8179566360759086,
                    "x2": -1.8706688391256094
                },
                {
                    "x1": 0.8943906462308358,
                    "x2": -2.256753541800084
                },
                {
                    "x1": -0.13915505697810085,
                    "x2": -1.9071924945818184
                },
                {
                    "x1": 0.28770106051161454,
                    "x2": -2.0812155855118735
                },
                {
                    "x1": -0.674519846177478,
                    "x2": -2.196292353285768
                },
                {
                    "x1": 0.22130984192108688,
                    "x2": -2.3337366435951363
                },
                {
                    "x1": 1.4550295831531128,
                    "x2": -2.245604135909923
                },
                {
                    "x1": -0.37006926127440665,
                    "x2": -2.116468975756574
                },
                {
                    "x1": -0.9636025852076151,
                    "x2": -2.0592514712308927
                },
                {
                    "x1": 1.9275627370504396,
                    "x2": -1.8308512595659003
                },
                {
                    "x1": 1.0654029461029901,
                    "x2": -2.271618457499597
                },
                {
                    "x1": -0.9324201231755156,
                    "x2": -2.2446415038647953
                },
                {
                    "x1": 1.1330223764253315,
                    "x2": -1.9687399528140597
                },
                {
                    "x1": 1.1827990423122703,
                    "x2": -1.9352500607354968
                },
                {
                    "x1": -0.2723080717568729,
                    "x2": -2.184692484110867
                },
                {
                    "x1": -0.737853399785759,
                    "x2": -2.0278698397756587
                },
                {
                    "x1": -0.026606211181398404,
                    "x2": -1.998549928703028
                },
                {
                    "x1": -0.11563559871476181,
                    "x2": -2.315826775973286
                },
                {
                    "x1": -0.9962126978466398,
                    "x2": -2.476623631325662
                },
                {
                    "x1": -0.7288929329445405,
                    "x2": -1.8934870810249367
                },
                {
                    "x1": -1.7464056388367206,
                    "x2": -2.3716303261170824
                },
                {
                    "x1": -1.3007745681742868,
                    "x2": -1.9544407094645393
                },
                {
                    "x1": -2.151974498473081,
                    "x2": -2.0112545821108347
                },
                {
                    "x1": -0.357525785204085,
                    "x2": -2.3522290391055227
                },
                {
                    "x1": -0.38709788581468374,
                    "x2": -2.1058116193310252
                },
                {
                    "x1": -1.3567381781308867,
                    "x2": -1.8824817821903128
                },
                {
                    "x1": 0.11825111192665505,
                    "x2": -2.3432074076536087
                },
                {
                    "x1": 0.7113568544852217,
                    "x2": -2.000377137313757
                },
                {
                    "x1": 0.43394469647880524,
                    "x2": -2.0746157438300963
                },
                {
                    "x1": -0.1748066064367817,
                    "x2": -1.823054466710669
                },
                {
                    "x1": -0.19584382828508787,
                    "x2": -2.1590998874109855
                },
                {
                    "x1": 0.4301459079841141,
                    "x2": -1.9487111556595924
                }
            ],
            "H2": [
                {
                    "x1": -0.6299339170488247,
                    "x2": 2.767405834163793
                },
                {
                    "x1": -2.278514215169912,
                    "x2": 2.649996827192922
                },
                {
                    "x1": -1.7891029971121923,
                    "x2": 2.5720054342605976
                },
                {
                    "x1": -0.2957935687953272,
                    "x2": 2.779788837189692
                },
                {
                    "x1": -1.1065137738492195,
                    "x2": 2.729059587354321
                },
                {
                    "x1": 0.9235513644725254,
                    "x2": 2.721778535120659
                }
            ],
            "H1": [
                {
                    "x1": -0.830871516713693,
                    "x2": 1.9164242526600277
                },
                {
                    "x1": -1.0050388571994215,
                    "x2": 2.030599740298532
                },
                {
                    "x1": -0.33136464737626187,
                    "x2": 1.9423111230870014
                },
                {
                    "x1": -0.5166811548341248,
                    "x2": 2.086499373473574
                },
                {
                    "x1": -0.3256920619375649,
                    "x2": 2.0632846757753573
                },
                {
                    "x1": -0.960205535308522,
                    "x2": 1.8738266500974272
                },
                {
                    "x1": -0.7847439859300689,
                    "x2": 2.371208917730686
                },
                {
                    "x1": 0.18492887624178767,
                    "x2": 1.8589057588675226
                },
                {
                    "x1": -1.0391182261509657,
                    "x2": 2.2202604372979473
                },
                {
                    "x1": -0.7909139122516333,
                    "x2": 2.011578370684348
                },
                {
                    "x1": 0.8813382170813193,
                    "x2": 2.482929799379789
                },
                {
                    "x1": -0.5136127789661791,
                    "x2": 2.4016079309197433
                },
                {
                    "x1": 0.6384908001758128,
                    "x2": 2.444972835978563
                },
                {
                    "x1": 0.8841001359110099,
                    "x2": 2.016418948749688
                },
                {
                    "x1": -0.9326219831459486,
                    "x2": 1.9998616214700349
                },
                {
                    "x1": 1.0137527484666256,
                    "x2": 1.8661043803798412
                },
                {
                    "x1": 0.4438508434107406,
                    "x2": 1.843676891730136
                },
                {
                    "x1": -0.1809304474833266,
                    "x2": 2.1373371450503975
                },
                {
                    "x1": 1.5676448498665343,
                    "x2": 2.1579102695805927
                },
                {
                    "x1": -0.8543267024468364,
                    "x2": 2.006132399922771
                },
                {
                    "x1": -0.6289353639431927,
                    "x2": 1.9525240703278681
                },
                {
                    "x1": -0.5785737560942658,
                    "x2": 2.5174971709370446
                },
                {
                    "x1": -0.2532253671523363,
                    "x2": 2.323665704792125
                },
                {
                    "x1": 0.8745314765448997,
                    "x2": 2.3126148572898084
                },
                {
                    "x1": -0.3681987883551341,
                    "x2": 1.9850841633436003
                }
            ],
            "H3": [
                {
                    "x1": 6.292450957054243,
                    "x2": 9.157049633049436
                },
                {
                    "x1": 6.849347488709529,
                    "x2": 8.056239528607632
                },
                {
                    "x1": 6.448401550033933,
                    "x2": 8.972554542226028
                },
                {
                    "x1": 4.327623761916106,
                    "x2": 9.319741610419936
                },
                {
                    "x1": 8.222576652220543,
                    "x2": 8.710581544532175
                },
                {
                    "x1": 6.484203823783212,
                    "x2": 8.959711603299823
                },
                {
                    "x1": 6.995076337059516,
                    "x2": 8.798535072791958
                },
                {
                    "x1": 7.605805614168475,
                    "x2": 8.801659643370721
                },
                {
                    "x1": 6.245262031299696,
                    "x2": 8.313591703118336
                },
                {
                    "x1": 8.602085586734685,
                    "x2": 9.293596107978134
                }
            ],
            "L2": [
                {
                    "x1": -0.7008665687838528,
                    "x2": -3.0015967628524325
                },
                {
                    "x1": -0.11925509917153308,
                    "x2": -2.663488408212937
                }
            ],
            "L3": [
                {
                    "x1": 0.26289010300519877,
                    "x2": -3.159505892009283
                }
            ]
        }
    },
    {
        "key": "x1",
        "variable": "x3",
        "metrics": {
            "x3__q1": 0.1531066141958941,
            "x3__q3": 0.10696155773352142,
            "x3__count": 2.6955843375750215,
            "x3__mean": -2.6220521544674997
        },
        "outliers": {
            "H1": [
                {
                    "x1": -0.9485040659135199,
                    "x3": 1.850977077397899
                },
                {
                    "x1": -0.13915505697810085,
                    "x3": 2.418140860466362
                },
                {
                    "x1": 0.7515949442848298,
                    "x3": 1.8965404762192941
                },
                {
                    "x1": -0.9267178667217677,
                    "x3": 2.1929002046761403
                },
                {
                    "x1": -1.2232882684064732,
                    "x3": 1.8690729972014952
                },
                {
                    "x1": 1.6533661610254564,
                    "x3": 1.9265517524026827
                },
                {
                    "x1": -0.593624090931504,
                    "x3": 1.9232930165033468
                },
                {
                    "x1": -0.7402812099814485,
                    "x3": 2.38259650779931
                },
                {
                    "x1": 0.16690117523071904,
                    "x3": 2.181108845982017
                },
                {
                    "x1": 0.7927443869602601,
                    "x3": 2.0180140289741937
                },
                {
                    "x1": 0.2899560045370407,
                    "x3": 2.261647036776984
                },
                {
                    "x1": -0.30214931842480475,
                    "x3": 1.8517360815608477
                },
                {
                    "x1": 0.41712438034530736,
                    "x3": 1.9583853886078202
                },
                {
                    "x1": -1.0330948161488018,
                    "x3": 1.961383008243379
                },
                {
                    "x1": -1.3265113911441069,
                    "x3": 1.83918189695968
                },
                {
                    "x1": 0.07127088421687526,
                    "x3": 2.027468261880386
                },
                {
                    "x1": -0.14525157960034615,
                    "x3": 1.9344716485517368
                },
                {
                    "x1": -0.20702799538635785,
                    "x3": 2.0117515348543265
                },
                {
                    "x1": 0.6690539187935528,
                    "x3": 1.8455399548936604
                },
                {
                    "x1": -0.6025884782713188,
                    "x3": 1.8259389152342969
                },
                {
                    "x1": 0.00783501967542229,
                    "x3": 1.8559328373749633
                },
                {
                    "x1": 0.3504844117204064,
                    "x3": 2.214864065585998
                },
                {
                    "x1": -1.6905238031118222,
                    "x3": 2.2411218395185264
                },
                {
                    "x1": -2.3411260488351915,
                    "x3": 1.8186891387775326
                },
                {
                    "x1": -0.39913227084155417,
                    "x3": 2.0294182964726337
                },
                {
                    "x1": -0.5250525577846669,
                    "x3": 1.944093934553661
                }
            ],
            "L2": [
                {
                    "x1": 0.10199973800709858,
                    "x3": -2.9201413977115127
                },
                {
                    "x1": -0.10108062082123813,
                    "x3": -2.4991492344858415
                },
                {
                    "x1": -0.04030678698387249,
                    "x3": -2.6220521544674997
                },
                {
                    "x1": 0.3087871195796025,
                    "x3": -2.4330386416454144
                },
                {
                    "x1": -0.7288929329445405,
                    "x3": -2.772068452531892
                },
                {
                    "x1": -1.3607723233897147,
                    "x3": -2.9133493351693915
                },
                {
                    "x1": 0.1437557531264604,
                    "x3": -2.712787421450937
                },
                {
                    "x1": -0.8543267024468364,
                    "x3": -2.587732385041522
                }
            ],
            "L1": [
                {
                    "x1": -1.4191247415862045,
                    "x3": -2.3368876258938776
                },
                {
                    "x1": 1.1381070389206922,
                    "x3": -2.360957974736525
                },
                {
                    "x1": 0.14698400177519164,
                    "x3": -2.1779763057217263
                },
                {
                    "x1": 0.21899734710728153,
                    "x3": -1.9685762408902268
                },
                {
                    "x1": -2.5568152364829055,
                    "x3": -2.069337971942999
                },
                {
                    "x1": -0.7117895685963371,
                    "x3": -1.9776836406485667
                },
                {
                    "x1": 0.8903738835303279,
                    "x3": -2.206010836331545
                },
                {
                    "x1": -0.7196212216796051,
                    "x3": -1.726008541441695
                },
                {
                    "x1": -3.0070037700734438,
                    "x3": -1.730580156372411
                },
                {
                    "x1": 0.2581190144709594,
                    "x3": -1.8292641230356357
                },
                {
                    "x1": 1.3511899166962384,
                    "x3": -1.7525532296146167
                },
                {
                    "x1": -1.1042552929007114,
                    "x3": -1.9072398273578335
                },
                {
                    "x1": 0.7328852232042984,
                    "x3": -1.8186179463243253
                },
                {
                    "x1": -2.243909789020351,
                    "x3": -2.090041290902784
                },
                {
                    "x1": 1.2730570934817724,
                    "x3": -1.7324318292329908
                },
                {
                    "x1": 0.19046311026346532,
                    "x3": -2.1930396440544064
                },
                {
                    "x1": -0.7351955970707906,
                    "x3": -2.0967920256084978
                },
                {
                    "x1": -1.0084340611260705,
                    "x3": -2.064436726680204
                },
                {
                    "x1": -1.2974934280917152,
                    "x3": -2.2198495746750244
                },
                {
                    "x1": 0.585369712347174,
                    "x3": -1.7790049591970558
                },
                {
                    "x1": -0.025006015074832452,
                    "x3": -2.375454951417037
                },
                {
                    "x1": 0.45332178154173186,
                    "x3": -1.842652238331238
                },
                {
                    "x1": 0.43220139933916274,
                    "x3": -2.1009313586043303
                },
                {
                    "x1": 0.27258981822999445,
                    "x3": -2.1060255152622522
                },
                {
                    "x1": -1.0324987937761911,
                    "x3": -1.7624848746838901
                },
                {
                    "x1": 0.6665178779549453,
                    "x3": -2.0880980131797067
                },
                {
                    "x1": -1.5202940549701702,
                    "x3": -1.8349909369192057
                },
                {
                    "x1": 1.596719388410072,
                    "x3": -1.9617323436184906
                }
            ],
            "H3": [
                {
                    "x1": 6.292450957054243,
                    "x3": 10.595118745616753
                },
                {
                    "x1": 6.849347488709529,
                    "x3": 9.960805793952636
                },
                {
                    "x1": 6.448401550033933,
                    "x3": 9.817926946321318
                },
                {
                    "x1": 4.327623761916106,
                    "x3": 11.68323968932216
                },
                {
                    "x1": -0.737853399785759,
                    "x3": 3.525793946007154
                },
                {
                    "x1": 8.222576652220543,
                    "x3": 9.683332970377903
                },
                {
                    "x1": 6.484203823783212,
                    "x3": 11.249551191255689
                },
                {
                    "x1": 6.995076337059516,
                    "x3": 10.483644128344128
                },
                {
                    "x1": 7.605805614168475,
                    "x3": 11.630283343752359
                },
                {
                    "x1": 6.245262031299696,
                    "x3": 12.689992360538431
                },
                {
                    "x1": 8.602085586734685,
                    "x3": 11.479419516535614
                }
            ],
            "H2": [
                {
                    "x1": -1.214420064287217,
                    "x3": 2.9639336673826846
                },
                {
                    "x1": 1.1395471866994589,
                    "x3": 2.6955843375750215
                },
                {
                    "x1": 1.2500971961669172,
                    "x3": 2.7667969473100356
                },
                {
                    "x1": -0.341343113978198,
                    "x3": 2.5409625257436104
                },
                {
                    "x1": 0.19301315382574716,
                    "x3": 2.582397975011784
                },
                {
                    "x1": -1.246953627803795,
                    "x3": 2.8488049578844215
                }
            ]
        }
    }
]
```
