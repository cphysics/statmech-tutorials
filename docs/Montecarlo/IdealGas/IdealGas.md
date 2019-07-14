
# Maxwell's distribution of speed.

#### Import


```python
import math as math
import random as random
import numpy as np
import matplotlib.pyplot as plt
```

#### Global constants


```python
m = 3.2  # mass is in unit of Kb
Kb = 1.0

```

#### Input parameters


```python
N = 100
u0 = 150.00
dv = 1.0
```

#### Starter 


```python
def starter(key):
    u = [0.0  for k in range(N)]
    
    if key == 0:return u
    else:
        for k in range(N):
            u[k] = u0
     
   
    return u
```

#### Hamiltonian


```python
def hamiltonian(u):
    H = 0.0
    for k in range(N):
          H = H + 0.5*u[k]**2
    return H
```

#### Pick a particle and change


```python
def pick_random_particle(printkey):
    n = random.randint(0, N-1)
    if printkey == 1: print "particle picked  at",n
    return n
```

#### Thermalization


```python
def thermalize(u,T,nruns,printkey):
    irun = 0
    h_stor = [0.0 for k in range(nrun)]
    while irun < nrun:
               L = len(u)
            
               h_old = hamiltonian(u)
              
               n = pick_random_particle(printkey)
               ov = u[n] 
               du = random.uniform(-dv,dv)
               u[n] = u[n] + du
              
                
               h_new = hamiltonian(u)
                
               dh = 0.5*m*(u[n]**2-ov**2)
               if printkey == 1:print  "=================", irun,"====================" 
                    
               if dh < 0:
                       
                        if printkey == 1: print irun, "Energy decreased! It is accepted!",dh
                        if printkey == 1: print irun, "old speed = ", ov,"replaced by",u[n] 
                            
                        h_stor[irun] = h_new
                       
               else:
                            
                       if printkey == 1:print irun, "Energy increased!",dh
                                
                       frac = math.exp(-dh/(Kb*T))
                       b = random.uniform(0.0,1.0)
                                
                       if printkey == 1:print "frac =",frac,"b =",b
                                    
                       if  b < frac:
                                        
                            if printkey == 1:print irun, "You Lucky"
                                
                            h_stor[irun] = h_new                             
                       else:
                                
                            if printkey == 1:print irun, "Loser"
                            if printkey == 1:print "speed restablished at", n, ":",u[n],"by",u[n]-du,"which is old",ov
                           
                            u[n]  = u[n] - du
                            h_stor[irun] = h_old 
                            
                            
              
               if u[n] != ov :                 
                   if printkey == 1:
                         print "Warning! speed changed at",n, ":", ov, " replaced by", u[n]        
                                    
               if printkey == 1:print  "---------------info-closed----------------"   
               if printkey == 1:print  ""                            
               if printkey == 2: print irun, h_stor[irun]   
                                                
               irun = irun +1
              
                   
    return h_stor,u
        
    
```

#### Simulation

#### Test


```python
N = 10
u = starter(1)
T = 300.0
nrun = 100
H,u = thermalize(u,T,nrun,1)
```

    particle picked  at 2
    ================= 0 ====================
    0 Energy increased! 5.16166800614
    frac = 0.982941610369 b = 0.296378524508
    0 You Lucky
    Warning! speed changed at 2 : 300.0  replaced by 300.017205067
    ---------------info-closed----------------
    
    particle picked  at 0
    ================= 1 ====================
    1 Energy increased! 23.3951734115
    frac = 0.924979308072 b = 0.607024790315
    1 You Lucky
    Warning! speed changed at 0 : 300.0  replaced by 300.077973778
    ---------------info-closed----------------
    
    particle picked  at 8
    ================= 2 ====================
    2 Energy decreased! It is accepted! -28.9376550483
    2 old speed =  300.0 replaced by 299.903525638
    Warning! speed changed at 8 : 300.0  replaced by 299.903525638
    ---------------info-closed----------------
    
    particle picked  at 0
    ================= 3 ====================
    3 Energy increased! 17.437958518
    frac = 0.943530556478 b = 0.639751221503
    3 You Lucky
    Warning! speed changed at 0 : 300.077973778  replaced by 300.136079577
    ---------------info-closed----------------
    
    particle picked  at 6
    ================= 4 ====================
    4 Energy decreased! It is accepted! -4.76002312716
    4 old speed =  300.0 replaced by 299.984132837
    Warning! speed changed at 6 : 300.0  replaced by 299.984132837
    ---------------info-closed----------------
    
    particle picked  at 4
    ================= 5 ====================
    5 Energy decreased! It is accepted! -23.0744788723
    5 old speed =  300.0 replaced by 299.923075208
    Warning! speed changed at 4 : 300.0  replaced by 299.923075208
    ---------------info-closed----------------
    
    particle picked  at 4
    ================= 6 ====================
    6 Energy decreased! It is accepted! -25.1873042255
    6 old speed =  299.923075208 replaced by 299.839084233
    Warning! speed changed at 4 : 299.923075208  replaced by 299.839084233
    ---------------info-closed----------------
    
    particle picked  at 8
    ================= 7 ====================
    7 Energy decreased! It is accepted! -23.5188848983
    7 old speed =  299.903525638 replaced by 299.82509388
    Warning! speed changed at 8 : 299.903525638  replaced by 299.82509388
    ---------------info-closed----------------
    
    particle picked  at 4
    ================= 8 ====================
    8 Energy increased! 3.66195450823
    frac = 0.987867682273 b = 0.901236906352
    8 You Lucky
    Warning! speed changed at 4 : 299.839084233  replaced by 299.85129705
    ---------------info-closed----------------
    
    particle picked  at 0
    ================= 9 ====================
    9 Energy decreased! It is accepted! -9.42665565287
    9 old speed =  300.136079577 replaced by 300.104669995
    Warning! speed changed at 0 : 300.136079577  replaced by 300.104669995
    ---------------info-closed----------------
    
    particle picked  at 4
    ================= 10 ====================
    10 Energy decreased! It is accepted! -1.94555000914
    10 old speed =  299.85129705 replaced by 299.844808597
    Warning! speed changed at 4 : 299.85129705  replaced by 299.844808597
    ---------------info-closed----------------
    
    particle picked  at 2
    ================= 11 ====================
    11 Energy decreased! It is accepted! -27.8179773732
    11 old speed =  300.017205067 replaced by 299.924469461
    Warning! speed changed at 2 : 300.017205067  replaced by 299.924469461
    ---------------info-closed----------------
    
    particle picked  at 7
    ================= 12 ====================
    12 Energy decreased! It is accepted! -15.7483746502
    12 old speed =  300.0 replaced by 299.947500824
    Warning! speed changed at 7 : 300.0  replaced by 299.947500824
    ---------------info-closed----------------
    
    particle picked  at 7
    ================= 13 ====================
    13 Energy increased! 16.6569944456
    frac = 0.945989967829 b = 0.855436607854
    13 You Lucky
    Warning! speed changed at 7 : 299.947500824  replaced by 300.003028717
    ---------------info-closed----------------
    
    particle picked  at 5
    ================= 14 ====================
    14 Energy increased! 13.5605829688
    frac = 0.955804444106 b = 0.462274377115
    14 You Lucky
    Warning! speed changed at 5 : 300.0  replaced by 300.045198538
    ---------------info-closed----------------
    
    particle picked  at 2
    ================= 15 ====================
    15 Energy decreased! It is accepted! -10.1659196052
    15 old speed =  299.924469461 replaced by 299.890572613
    Warning! speed changed at 2 : 299.924469461  replaced by 299.890572613
    ---------------info-closed----------------
    
    particle picked  at 2
    ================= 16 ====================
    16 Energy increased! 13.1461147765
    frac = 0.957125858504 b = 0.0764044163788
    16 You Lucky
    Warning! speed changed at 2 : 299.890572613  replaced by 299.934405782
    ---------------info-closed----------------
    
    particle picked  at 6
    ================= 17 ====================
    17 Energy increased! 16.0662962599
    frac = 0.947854451331 b = 0.311728441504
    17 You Lucky
    Warning! speed changed at 6 : 299.984132837  replaced by 300.03768521
    ---------------info-closed----------------
    
    particle picked  at 0
    ================= 18 ====================
    18 Energy increased! 14.9157901932
    frac = 0.951496471466 b = 0.778044719102
    18 You Lucky
    Warning! speed changed at 0 : 300.104669995  replaced by 300.154367839
    ---------------info-closed----------------
    
    particle picked  at 5
    ================= 19 ====================
    19 Energy increased! 0.212891347102
    frac = 0.99929061391 b = 0.600347076825
    19 You Lucky
    Warning! speed changed at 5 : 300.045198538  replaced by 300.045908068
    ---------------info-closed----------------
    
    particle picked  at 7
    ================= 20 ====================
    20 Energy increased! 5.6356927141
    frac = 0.981389708059 b = 0.962471313504
    20 You Lucky
    Warning! speed changed at 7 : 300.003028717  replaced by 300.021813582
    ---------------info-closed----------------
    
    particle picked  at 8
    ================= 21 ====================
    21 Energy decreased! It is accepted! -0.361216020458
    21 old speed =  299.82509388 replaced by 299.823889122
    Warning! speed changed at 8 : 299.82509388  replaced by 299.823889122
    ---------------info-closed----------------
    
    particle picked  at 8
    ================= 22 ====================
    22 Energy increased! 9.18340368766
    frac = 0.969852437229 b = 0.910312616567
    22 You Lucky
    Warning! speed changed at 8 : 299.823889122  replaced by 299.854516884
    ---------------info-closed----------------
    
    particle picked  at 2
    ================= 23 ====================
    23 Energy decreased! It is accepted! -15.3415660895
    23 old speed =  299.934405782 replaced by 299.883251682
    Warning! speed changed at 2 : 299.934405782  replaced by 299.883251682
    ---------------info-closed----------------
    
    particle picked  at 3
    ================= 24 ====================
    24 Energy decreased! It is accepted! -29.9420272373
    24 old speed =  300.0 replaced by 299.900176635
    Warning! speed changed at 3 : 300.0  replaced by 299.900176635
    ---------------info-closed----------------
    
    particle picked  at 1
    ================= 25 ====================
    25 Energy increased! 3.67190862696
    frac = 0.987834904977 b = 0.85142877576
    25 You Lucky
    Warning! speed changed at 1 : 300.0  replaced by 300.012239446
    ---------------info-closed----------------
    
    particle picked  at 0
    ================= 26 ====================
    26 Energy decreased! It is accepted! -28.9294825618
    26 old speed =  300.154367839 replaced by 300.057970345
    Warning! speed changed at 0 : 300.154367839  replaced by 300.057970345
    ---------------info-closed----------------
    
    particle picked  at 0
    ================= 27 ====================
    27 Energy decreased! It is accepted! -17.5218772821
    27 old speed =  300.057970345 replaced by 299.999569688
    Warning! speed changed at 0 : 300.057970345  replaced by 299.999569688
    ---------------info-closed----------------
    
    particle picked  at 1
    ================= 28 ====================
    28 Energy increased! 10.987743112
    frac = 0.964036800437 b = 0.354706880466
    28 You Lucky
    Warning! speed changed at 1 : 300.012239446  replaced by 300.048861527
    ---------------info-closed----------------
    
    particle picked  at 2
    ================= 29 ====================
    29 Energy decreased! It is accepted! -23.0555321212
    29 old speed =  299.883251682 replaced by 299.806360131
    Warning! speed changed at 2 : 299.883251682  replaced by 299.806360131
    ---------------info-closed----------------
    
    particle picked  at 0
    ================= 30 ====================
    30 Energy increased! 14.56813825
    frac = 0.95259974259 b = 0.992217091382
    30 Loser
    speed restablished at 0 : 300.048126289 by 299.999569688 which is old 299.999569688
    ---------------info-closed----------------
    
    particle picked  at 4
    ================= 31 ====================
    31 Energy decreased! It is accepted! -19.1459640601
    31 old speed =  299.844808597 replaced by 299.780948885
    Warning! speed changed at 4 : 299.844808597  replaced by 299.780948885
    ---------------info-closed----------------
    
    particle picked  at 2
    ================= 32 ====================
    32 Energy increased! 10.3893583094
    frac = 0.965961602654 b = 0.0652759977248
    32 You Lucky
    Warning! speed changed at 2 : 299.806360131  replaced by 299.841011691
    ---------------info-closed----------------
    
    particle picked  at 5
    ================= 33 ====================
    33 Energy increased! 27.6413736072
    frac = 0.911979367951 b = 0.925790017225
    33 Loser
    speed restablished at 5 : 300.138017745 by 300.045908068 which is old 300.045908068
    ---------------info-closed----------------
    
    particle picked  at 3
    ================= 34 ====================
    34 Energy increased! 6.48585504453
    frac = 0.978612509829 b = 0.639748903698
    34 You Lucky
    Warning! speed changed at 3 : 299.900176635  replaced by 299.921802568
    ---------------info-closed----------------
    
    particle picked  at 5
    ================= 35 ====================
    35 Energy decreased! It is accepted! -26.3949101618
    35 old speed =  300.045908068 replaced by 299.957925597
    Warning! speed changed at 5 : 300.045908068  replaced by 299.957925597
    ---------------info-closed----------------
    
    particle picked  at 5
    ================= 36 ====================
    36 Energy increased! 13.992910126
    frac = 0.954428035382 b = 0.00198934609112
    36 You Lucky
    Warning! speed changed at 5 : 299.957925597  replaced by 300.004571546
    ---------------info-closed----------------
    
    particle picked  at 5
    ================= 37 ====================
    37 Energy decreased! It is accepted! -18.5791926362
    37 old speed =  300.004571546 replaced by 299.942635454
    Warning! speed changed at 5 : 300.004571546  replaced by 299.942635454
    ---------------info-closed----------------
    
    particle picked  at 5
    ================= 38 ====================
    38 Energy increased! 19.0993831631
    frac = 0.93831964928 b = 0.684421660523
    38 You Lucky
    Warning! speed changed at 5 : 299.942635454  replaced by 300.006305483
    ---------------info-closed----------------
    
    particle picked  at 3
    ================= 39 ====================
    39 Energy increased! 12.6217197065
    frac = 0.958800361851 b = 0.978536469383
    39 Loser
    speed restablished at 3 : 299.963882984 by 299.921802568 which is old 299.921802568
    ---------------info-closed----------------
    
    particle picked  at 0
    ================= 40 ====================
    40 Energy decreased! It is accepted! -24.2180688647
    40 old speed =  299.999569688 replaced by 299.918831812
    Warning! speed changed at 0 : 299.999569688  replaced by 299.918831812
    ---------------info-closed----------------
    
    particle picked  at 3
    ================= 41 ====================
    41 Energy decreased! It is accepted! -4.27460233111
    41 old speed =  299.921802568 replaced by 299.90754984
    Warning! speed changed at 3 : 299.921802568  replaced by 299.90754984
    ---------------info-closed----------------
    
    particle picked  at 3
    ================= 42 ====================
    42 Energy increased! 10.8331681318
    frac = 0.964533648324 b = 0.980522343152
    42 Loser
    speed restablished at 3 : 299.943669357 by 299.90754984 which is old 299.90754984
    ---------------info-closed----------------
    
    particle picked  at 2
    ================= 43 ====================
    43 Energy decreased! It is accepted! -0.620556065638
    43 old speed =  299.841011691 replaced by 299.838942067
    Warning! speed changed at 2 : 299.841011691  replaced by 299.838942067
    ---------------info-closed----------------
    
    particle picked  at 3
    ================= 44 ====================
    44 Energy increased! 21.5404667892
    frac = 0.930715572441 b = 0.255181673312
    44 You Lucky
    Warning! speed changed at 3 : 299.90754984  replaced by 299.979364931
    ---------------info-closed----------------
    
    particle picked  at 4
    ================= 45 ====================
    45 Energy increased! 6.331827505
    frac = 0.979115083092 b = 0.535424245741
    45 You Lucky
    Warning! speed changed at 4 : 299.780948885  replaced by 299.802069655
    ---------------info-closed----------------
    
    particle picked  at 4
    ================= 46 ====================
    46 Energy increased! 9.67196917396
    frac = 0.968274267884 b = 0.448130433025
    46 You Lucky
    Warning! speed changed at 4 : 299.802069655  replaced by 299.834329102
    ---------------info-closed----------------
    
    particle picked  at 1
    ================= 47 ====================
    47 Energy decreased! It is accepted! -22.1880505342
    47 old speed =  300.048861527 replaced by 299.974904288
    Warning! speed changed at 1 : 300.048861527  replaced by 299.974904288
    ---------------info-closed----------------
    
    particle picked  at 0
    ================= 48 ====================
    48 Energy decreased! It is accepted! -26.4379926945
    48 old speed =  299.918831812 replaced by 299.830668362
    Warning! speed changed at 0 : 299.918831812  replaced by 299.830668362
    ---------------info-closed----------------
    
    particle picked  at 5
    ================= 49 ====================
    49 Energy decreased! It is accepted! -17.6255352389
    49 old speed =  300.006305483 replaced by 299.94754918
    Warning! speed changed at 5 : 300.006305483  replaced by 299.94754918
    ---------------info-closed----------------
    
    particle picked  at 5
    ================= 50 ====================
    50 Energy increased! 26.9557187349
    frac = 0.914066095325 b = 0.216679528733
    50 You Lucky
    Warning! speed changed at 5 : 299.94754918  replaced by 300.037403829
    ---------------info-closed----------------
    
    particle picked  at 8
    ================= 51 ====================
    51 Energy decreased! It is accepted! -27.966674026
    51 old speed =  299.854516884 replaced by 299.761234898
    Warning! speed changed at 8 : 299.854516884  replaced by 299.761234898
    ---------------info-closed----------------
    
    particle picked  at 2
    ================= 52 ====================
    52 Energy decreased! It is accepted! -22.2578037851
    52 old speed =  299.838942067 replaced by 299.764700344
    Warning! speed changed at 2 : 299.838942067  replaced by 299.764700344
    ---------------info-closed----------------
    
    particle picked  at 1
    ================= 53 ====================
    53 Energy increased! 1.8452384392
    frac = 0.993868082617 b = 0.932817295881
    53 You Lucky
    Warning! speed changed at 1 : 299.974904288  replaced by 299.981055534
    ---------------info-closed----------------
    
    particle picked  at 6
    ================= 54 ====================
    54 Energy increased! 12.3385972816
    frac = 0.959705648574 b = 0.262262734931
    54 You Lucky
    Warning! speed changed at 6 : 300.03768521  replaced by 300.078805884
    ---------------info-closed----------------
    
    particle picked  at 4
    ================= 55 ====================
    55 Energy increased! 17.1512405735
    frac = 0.944432744672 b = 0.868938895111
    55 You Lucky
    Warning! speed changed at 4 : 299.834329102  replaced by 299.891526038
    ---------------info-closed----------------
    
    particle picked  at 5
    ================= 56 ====================
    56 Energy decreased! It is accepted! -1.43622642083
    56 old speed =  300.037403829 replaced by 300.032616966
    Warning! speed changed at 5 : 300.037403829  replaced by 300.032616966
    ---------------info-closed----------------
    
    particle picked  at 3
    ================= 57 ====================
    57 Energy decreased! It is accepted! -26.2834912367
    57 old speed =  299.979364931 replaced by 299.891734468
    Warning! speed changed at 3 : 299.979364931  replaced by 299.891734468
    ---------------info-closed----------------
    
    particle picked  at 5
    ================= 58 ====================
    58 Energy increased! 10.2306393701
    frac = 0.966472792538 b = 0.0967580124621
    58 You Lucky
    Warning! speed changed at 5 : 300.032616966  replaced by 300.066713453
    ---------------info-closed----------------
    
    particle picked  at 4
    ================= 59 ====================
    59 Energy decreased! It is accepted! -14.4982905504
    59 old speed =  299.891526038 replaced by 299.843177024
    Warning! speed changed at 4 : 299.891526038  replaced by 299.843177024
    ---------------info-closed----------------
    
    particle picked  at 7
    ================= 60 ====================
    60 Energy decreased! It is accepted! -3.0215758524
    60 old speed =  300.021813582 replaced by 300.011742226
    Warning! speed changed at 7 : 300.021813582  replaced by 300.011742226
    ---------------info-closed----------------
    
    particle picked  at 3
    ================= 61 ====================
    61 Energy decreased! It is accepted! -19.1549554404
    61 old speed =  299.891734468 replaced by 299.827854762
    Warning! speed changed at 3 : 299.891734468  replaced by 299.827854762
    ---------------info-closed----------------
    
    particle picked  at 8
    ================= 62 ====================
    62 Energy decreased! It is accepted! -22.0943850821
    62 old speed =  299.761234898 replaced by 299.687519222
    Warning! speed changed at 8 : 299.761234898  replaced by 299.687519222
    ---------------info-closed----------------
    
    particle picked  at 7
    ================= 63 ====================
    63 Energy increased! 23.4692149725
    frac = 0.924751046535 b = 0.598788195177
    63 You Lucky
    Warning! speed changed at 7 : 300.011742226  replaced by 300.089959684
    ---------------info-closed----------------
    
    particle picked  at 3
    ================= 64 ====================
    64 Energy decreased! It is accepted! -25.1329730987
    64 old speed =  299.827854762 replaced by 299.744018364
    Warning! speed changed at 3 : 299.827854762  replaced by 299.744018364
    ---------------info-closed----------------
    
    particle picked  at 7
    ================= 65 ====================
    65 Energy decreased! It is accepted! -5.85495081207
    65 old speed =  300.089959684 replaced by 300.070448398
    Warning! speed changed at 7 : 300.089959684  replaced by 300.070448398
    ---------------info-closed----------------
    
    particle picked  at 4
    ================= 66 ====================
    66 Energy decreased! It is accepted! -11.9237115371
    66 old speed =  299.843177024 replaced by 299.803407894
    Warning! speed changed at 4 : 299.843177024  replaced by 299.803407894
    ---------------info-closed----------------
    
    particle picked  at 3
    ================= 67 ====================
    67 Energy increased! 19.6136743676
    frac = 0.936712462135 b = 0.325069421187
    67 You Lucky
    Warning! speed changed at 3 : 299.744018364  replaced by 299.809445971
    ---------------info-closed----------------
    
    particle picked  at 1
    ================= 68 ====================
    68 Energy increased! 7.15489674693
    frac = 0.976432499664 b = 0.945742642271
    68 You Lucky
    Warning! speed changed at 1 : 299.981055534  replaced by 300.004905748
    ---------------info-closed----------------
    
    particle picked  at 5
    ================= 69 ====================
    69 Energy increased! 6.05425179895
    frac = 0.980021430862 b = 0.140633653769
    69 You Lucky
    Warning! speed changed at 5 : 300.066713453  replaced by 300.086889127
    ---------------info-closed----------------
    
    particle picked  at 4
    ================= 70 ====================
    70 Energy increased! 8.52121746445
    frac = 0.97199554466 b = 0.731585384514
    70 You Lucky
    Warning! speed changed at 4 : 299.803407894  replaced by 299.831829231
    ---------------info-closed----------------
    
    particle picked  at 5
    ================= 71 ====================
    71 Energy increased! 28.7402147762
    frac = 0.908645076525 b = 0.3751527247
    71 You Lucky
    Warning! speed changed at 5 : 300.086889127  replaced by 300.182646826
    ---------------info-closed----------------
    
    particle picked  at 0
    ================= 72 ====================
    72 Energy decreased! It is accepted! -15.5910831236
    72 old speed =  299.830668362 replaced by 299.778664224
    Warning! speed changed at 0 : 299.830668362  replaced by 299.778664224
    ---------------info-closed----------------
    
    particle picked  at 4
    ================= 73 ====================
    73 Energy decreased! It is accepted! -1.36859774486
    73 old speed =  299.831829231 replaced by 299.827264645
    Warning! speed changed at 4 : 299.831829231  replaced by 299.827264645
    ---------------info-closed----------------
    
    particle picked  at 7
    ================= 74 ====================
    74 Energy increased! 13.8151893339
    frac = 0.954993608577 b = 0.261501372311
    74 You Lucky
    Warning! speed changed at 7 : 300.070448398  replaced by 300.116484686
    ---------------info-closed----------------
    
    particle picked  at 6
    ================= 75 ====================
    75 Energy decreased! It is accepted! -28.8318446459
    75 old speed =  300.078805884 replaced by 299.982709588
    Warning! speed changed at 6 : 300.078805884  replaced by 299.982709588
    ---------------info-closed----------------
    
    particle picked  at 3
    ================= 76 ====================
    76 Energy increased! 11.3434231571
    frac = 0.962894515542 b = 0.106283361727
    76 You Lucky
    Warning! speed changed at 3 : 299.809445971  replaced by 299.847279027
    ---------------info-closed----------------
    
    particle picked  at 8
    ================= 77 ====================
    77 Energy decreased! It is accepted! -2.85497555201
    77 old speed =  299.687519222 replaced by 299.677992562
    Warning! speed changed at 8 : 299.687519222  replaced by 299.677992562
    ---------------info-closed----------------
    
    particle picked  at 0
    ================= 78 ====================
    78 Energy decreased! It is accepted! -18.3217662101
    78 old speed =  299.778664224 replaced by 299.717540347
    Warning! speed changed at 0 : 299.778664224  replaced by 299.717540347
    ---------------info-closed----------------
    
    particle picked  at 8
    ================= 79 ====================
    79 Energy decreased! It is accepted! -10.5712767165
    79 old speed =  299.677992562 replaced by 299.642715034
    Warning! speed changed at 8 : 299.677992562  replaced by 299.642715034
    ---------------info-closed----------------
    
    particle picked  at 6
    ================= 80 ====================
    80 Energy increased! 25.8981647079
    frac = 0.917294029106 b = 0.377103705486
    80 You Lucky
    Warning! speed changed at 6 : 299.982709588  replaced by 300.06902936
    ---------------info-closed----------------
    
    particle picked  at 3
    ================= 81 ====================
    81 Energy increased! 3.4098065182
    frac = 0.988698327469 b = 0.0312159171229
    81 You Lucky
    Warning! speed changed at 3 : 299.847279027  replaced by 299.858650622
    ---------------info-closed----------------
    
    particle picked  at 8
    ================= 82 ====================
    82 Energy decreased! It is accepted! -18.4628674863
    82 old speed =  299.642715034 replaced by 299.581092424
    Warning! speed changed at 8 : 299.642715034  replaced by 299.581092424
    ---------------info-closed----------------
    
    particle picked  at 7
    ================= 83 ====================
    83 Energy decreased! It is accepted! -7.46450814405
    83 old speed =  300.116484686 replaced by 300.091611619
    Warning! speed changed at 7 : 300.116484686  replaced by 300.091611619
    ---------------info-closed----------------
    
    particle picked  at 4
    ================= 84 ====================
    84 Energy increased! 9.49589463838
    frac = 0.968842729494 b = 0.108661874014
    84 You Lucky
    Warning! speed changed at 4 : 299.827264645  replaced by 299.85893419
    ---------------info-closed----------------
    
    particle picked  at 1
    ================= 85 ====================
    85 Energy increased! 10.4225579484
    frac = 0.965854709981 b = 0.114826465239
    85 You Lucky
    Warning! speed changed at 1 : 300.004905748  replaced by 300.039645028
    ---------------info-closed----------------
    
    particle picked  at 8
    ================= 86 ====================
    86 Energy decreased! It is accepted! -22.7336433515
    86 old speed =  299.581092424 replaced by 299.505198037
    Warning! speed changed at 8 : 299.581092424  replaced by 299.505198037
    ---------------info-closed----------------
    
    particle picked  at 0
    ================= 87 ====================
    87 Energy increased! 1.00243789502
    frac = 0.996664116813 b = 0.41737453119
    87 You Lucky
    Warning! speed changed at 0 : 299.717540347  replaced by 299.720884937
    ---------------info-closed----------------
    
    particle picked  at 3
    ================= 88 ====================
    88 Energy decreased! It is accepted! -3.63974961165
    88 old speed =  299.858650622 replaced by 299.846512159
    Warning! speed changed at 3 : 299.858650622  replaced by 299.846512159
    ---------------info-closed----------------
    
    particle picked  at 2
    ================= 89 ====================
    89 Energy increased! 5.00314272899
    frac = 0.983461151261 b = 0.258379389692
    89 You Lucky
    Warning! speed changed at 2 : 299.764700344  replaced by 299.781390112
    ---------------info-closed----------------
    
    particle picked  at 5
    ================= 90 ====================
    90 Energy increased! 14.0127474497
    frac = 0.954364926476 b = 0.54718777645
    90 You Lucky
    Warning! speed changed at 5 : 300.182646826  replaced by 300.229323935
    ---------------info-closed----------------
    
    particle picked  at 6
    ================= 91 ====================
    91 Energy increased! 27.3160839095
    frac = 0.912968762564 b = 0.466057239774
    91 You Lucky
    Warning! speed changed at 6 : 300.06902936  replaced by 300.160048222
    ---------------info-closed----------------
    
    particle picked  at 4
    ================= 92 ====================
    92 Energy increased! 9.30101604776
    frac = 0.969472289637 b = 0.207884505864
    92 You Lucky
    Warning! speed changed at 4 : 299.85893419  replaced by 299.889950558
    ---------------info-closed----------------
    
    particle picked  at 7
    ================= 93 ====================
    93 Energy decreased! It is accepted! -17.9480064066
    93 old speed =  300.091611619 replaced by 300.031797234
    Warning! speed changed at 7 : 300.091611619  replaced by 300.031797234
    ---------------info-closed----------------
    
    particle picked  at 8
    ================= 94 ====================
    94 Energy increased! 16.6307891095
    frac = 0.946072604722 b = 0.68023491431
    94 You Lucky
    Warning! speed changed at 8 : 299.505198037  replaced by 299.560720438
    ---------------info-closed----------------
    
    particle picked  at 8
    ================= 95 ====================
    95 Energy decreased! It is accepted! -7.31052968793
    95 old speed =  299.560720438 replaced by 299.536315277
    Warning! speed changed at 8 : 299.560720438  replaced by 299.536315277
    ---------------info-closed----------------
    
    particle picked  at 6
    ================= 96 ====================
    96 Energy decreased! It is accepted! -17.3938902654
    96 old speed =  300.160048222 replaced by 300.102093908
    Warning! speed changed at 6 : 300.160048222  replaced by 300.102093908
    ---------------info-closed----------------
    
    particle picked  at 5
    ================= 97 ====================
    97 Energy decreased! It is accepted! -15.6593938539
    97 old speed =  300.229323935 replaced by 300.177161295
    Warning! speed changed at 5 : 300.229323935  replaced by 300.177161295
    ---------------info-closed----------------
    
    particle picked  at 0
    ================= 98 ====================
    98 Energy decreased! It is accepted! -28.3977836631
    98 old speed =  299.720884937 replaced by 299.626122526
    Warning! speed changed at 0 : 299.720884937  replaced by 299.626122526
    ---------------info-closed----------------
    
    particle picked  at 1
    ================= 99 ====================
    99 Energy decreased! It is accepted! -11.2829622779
    99 old speed =  300.039645028 replaced by 300.002037767
    Warning! speed changed at 1 : 300.039645028  replaced by 300.002037767
    ---------------info-closed----------------
    
    [299.6261225259406, 300.00203776661704, 299.781390112132, 299.8465121588739, 299.8899505582405, 300.1771612945372, 300.10209390845785, 300.03179723356243, 299.5363152772222, 300.0]



```python
N = 1000
u = starter(1)
T = 300.0
nrun = 100000
H,u = thermalize(u,T,nrun,0)

X = np.arange(0,len(H),1)
plt.figure(1)
plt.grid()
plt.plot(X,H,"-")
plt.show()     
            
```


![png](output_18_0.png)


#### Speed Distribution


```python

num_bins = 20
plt.figure(1)
plt.hist(u,num_bins, normed= 1.0, facecolor='green', alpha = 0.5)
plt.grid()
plt.show()
```


![png](output_20_0.png)



```python
u
```




    [152.53697392059593,
     128.31327589246823,
     140.436851808329,
     132.80382195754856,
     132.31407886817632,
     135.32050027807352,
     130.798459146321,
     129.09134596606734,
     135.03752198248986,
     141.62112963823625,
     138.27767642774265,
     130.71831125303953,
     136.86307540872224,
     121.34978066101247,
     132.73412663344874,
     131.8941976189342,
     132.94590280465187,
     139.99718986540782,
     126.30367606031899,
     136.6624201750959,
     134.71470758065294,
     140.22618602838844,
     128.3421710555995,
     131.18971363418476,
     137.2949504313762,
     133.9325213791171,
     132.3273444604972,
     137.01728024575485,
     138.7334279327667,
     131.73728297436287,
     142.15692647221064,
     131.59890748025197,
     129.69685418478122,
     130.3928982697706,
     133.33851141189984,
     135.70859014741555,
     139.5686898092376,
     130.42623900237018,
     138.1549314213626,
     134.1047535200175,
     134.11292649015837,
     125.42388153155485,
     124.57194118622577,
     131.7017625657973,
     129.20683563575193,
     128.04132499785734,
     130.85720902190866,
     137.82826258554866,
     133.4575684897915,
     137.74183777291927,
     132.4773493776854,
     127.80113465662937,
     136.75961609875358,
     134.02724421675092,
     135.00323622662827,
     136.60789546569578,
     125.35329383850176,
     134.1023584734773,
     137.0722197122356,
     139.96349822660508,
     134.11388102076194,
     137.78437853184,
     133.1490214372556,
     138.3024293767515,
     140.2474824710941,
     133.1865677976496,
     135.21197961798862,
     130.68799268977372,
     136.86249221917038,
     135.78134627417637,
     141.35163595663747,
     138.62137316754215,
     129.49970895942786,
     137.80508486126357,
     132.7855147828327,
     132.69701198534113,
     134.293914064531,
     138.13570287905537,
     133.93454715574518,
     132.37891955733335,
     136.6798469793762,
     133.41276957904762,
     137.51371047747227,
     133.65857668805802,
     123.85131731169427,
     129.391466893309,
     133.3909979802819,
     144.06316076184086,
     137.8664370849281,
     128.2375880846792,
     140.44862493306996,
     133.08921447679677,
     138.2105296201541,
     135.18243128580713,
     137.62782519548216,
     136.27893012420037,
     132.78748369907333,
     136.7765860746624,
     136.56845749699295,
     144.22950291281842,
     140.56092223209336,
     130.13855757583917,
     135.9198500520115,
     135.11083426122389,
     130.9169846736974,
     132.42342214295036,
     141.5334395491123,
     141.4139275019023,
     142.3287926940169,
     126.06129381026435,
     129.86281170228267,
     128.40243941806722,
     134.71802868838208,
     134.11588977597893,
     121.0692404655156,
     136.3531498450009,
     135.3991625542293,
     138.3536916275517,
     132.82970264542374,
     125.9369676064337,
     137.22383820845184,
     123.79315137007481,
     139.0822701341406,
     136.42887013312557,
     137.82728430971957,
     132.60834897662448,
     131.59156460820878,
     132.35581654990125,
     131.81399407592244,
     134.75348804821417,
     131.52496126422605,
     124.41674508789325,
     136.32473006853132,
     134.92203448652273,
     135.5202955221366,
     130.39278453265538,
     131.3893923018346,
     129.6964667339928,
     136.68971488254945,
     138.40024191953412,
     135.5384850909171,
     135.5298128887677,
     130.9681136951003,
     148.9695749458498,
     138.65622193713517,
     134.24148627342186,
     126.37290362543185,
     136.52355980093503,
     136.90290057754098,
     135.24119406033046,
     132.29185836353608,
     148.02566201517843,
     133.06298190744295,
     129.13255682540114,
     131.7476042068434,
     132.49355253889348,
     130.04611959809213,
     132.5477545085171,
     136.06793582988075,
     132.24598855495316,
     135.75582977601223,
     129.51247977898944,
     135.96978529232263,
     129.60536083064153,
     131.3811236689462,
     130.10544346547357,
     128.28536316091055,
     136.31608248146253,
     140.83134461569082,
     134.48353554060637,
     131.44857800180603,
     134.78441830784197,
     137.46766557631904,
     134.2547355047766,
     124.54224922599717,
     128.15444120967302,
     134.44755078830124,
     131.6817151281141,
     129.78294904975965,
     134.40333466905466,
     132.2665437777386,
     136.9397146557049,
     129.1586611818881,
     133.31063584701496,
     134.1813839443107,
     128.16108159535776,
     134.80904811469023,
     132.52271445493943,
     132.49137181783996,
     132.03293517402997,
     136.33036793345235,
     137.8258309260236,
     136.02590968257303,
     130.32962196281116,
     138.27507751953266,
     134.8630654268092,
     135.3641605111605,
     133.7225134325253,
     134.5240770562576,
     140.04481268901048,
     135.11621234725717,
     133.5290903925507,
     128.54389187091917,
     144.08243649066947,
     136.90009437815004,
     137.08042161705825,
     137.5507514703105,
     131.28150300348216,
     136.30216027648302,
     139.28769630317868,
     136.07652355102886,
     137.6505286293463,
     133.77802944457932,
     135.42914314500467,
     135.0123386649573,
     138.967304479209,
     134.93819196421714,
     134.58675710133323,
     138.37767631589648,
     127.1681584812201,
     127.47590837784763,
     137.7596848891184,
     128.80244195115898,
     139.8951736929954,
     134.7665709079596,
     130.3322741583445,
     129.6207703397924,
     142.44704584370368,
     130.69370641481623,
     135.6465712262506,
     129.8889015341072,
     134.81586859771903,
     135.29146744985704,
     135.79346262431338,
     127.17173591468108,
     134.29163907549847,
     134.31536632578704,
     141.0318590152523,
     138.98378041149232,
     141.2453756707175,
     135.33386559928624,
     137.77675136889272,
     142.90320603089285,
     135.15957889767256,
     129.58837887024563,
     135.01653697822988,
     138.1280611822878,
     137.81286171542988,
     137.87864598257548,
     132.36197577637404,
     135.34643613220186,
     137.08802870786525,
     134.25593431017526,
     140.0965941012118,
     136.1354531498805,
     139.60173874031628,
     142.1884424795718,
     139.4282077859784,
     140.4378223480546,
     141.14394203276737,
     134.80157884536197,
     130.2120302488567,
     133.12849755223328,
     126.76422473110674,
     141.29123603504758,
     136.94088037629103,
     131.21799468909555,
     135.5830395095889,
     134.42644594991577,
     133.00249925370116,
     134.1279227141204,
     136.68806217714155,
     128.3299311767685,
     134.42675228077027,
     134.33285848249827,
     138.2004587361354,
     132.5232562517257,
     135.5673829013085,
     136.06083792562427,
     129.92612202158958,
     132.2476151140744,
     133.35669087064448,
     137.79355670155505,
     133.07295921064375,
     131.30588172460003,
     123.54245272298101,
     131.8802736088557,
     132.02313506622474,
     134.01662098974492,
     135.01522474996457,
     129.88425787636987,
     132.2947266708029,
     133.26795114295314,
     137.76059681837302,
     140.43201451383968,
     123.77164688119001,
     134.5942140729307,
     134.72116339724283,
     137.81311383298865,
     137.1993623203678,
     135.50907447438172,
     142.12740435659185,
     130.61244669277613,
     140.92486869278636,
     135.79383387159103,
     140.1065127468415,
     131.53815255562918,
     131.83792337563588,
     131.8816719901831,
     136.42173721657878,
     140.72406761890096,
     134.32033750845582,
     137.4947327261507,
     132.73434294925417,
     134.33078877573985,
     135.18754156573803,
     135.45984263053802,
     134.95801301354484,
     135.81238348494213,
     135.16313187223415,
     128.4703251407475,
     143.37140512194648,
     131.86158306606674,
     134.5572786880074,
     133.37087242546468,
     137.26640148054284,
     142.62283719898272,
     136.00583530393317,
     135.95797717688635,
     132.23307255718495,
     139.16423396514304,
     139.586720872186,
     138.48591119741064,
     132.13429162953187,
     132.35678744150167,
     135.13584027342685,
     134.23846626588394,
     133.60934125156294,
     134.7053084065632,
     132.3265435926093,
     123.45189996966262,
     127.2278034802087,
     135.61574268403476,
     134.46353912735393,
     131.76295229252878,
     129.66632110456493,
     138.61806591326965,
     139.0747427236818,
     139.76970385521398,
     138.08322858952988,
     133.02807095717716,
     133.7435520250619,
     136.6894726280003,
     136.6906132642527,
     135.96647775504152,
     134.96130805017208,
     128.86350803859952,
     138.20995328105911,
     132.75597591971103,
     128.1030187967407,
     133.92147688014128,
     139.99771320505448,
     134.50698690293018,
     141.5260708947022,
     138.30126038473236,
     136.02280268926395,
     135.28569436060246,
     133.812855718125,
     128.35377565521077,
     136.09772285875437,
     139.6221924643782,
     132.72891940931677,
     149.26088055768352,
     135.1535249320635,
     135.35801387513814,
     133.01799074681944,
     135.1789223427826,
     136.35260863985746,
     135.20832113603288,
     127.28015976092442,
     137.60502507556475,
     137.64613697459254,
     133.66967706037607,
     134.61273621807152,
     135.49351896379142,
     136.52156651304836,
     134.73145852887276,
     135.30944870432333,
     139.63808492700113,
     133.71192114705494,
     139.11612120980905,
     133.79214122763426,
     134.42769640829084,
     138.78810924039666,
     134.67726714111905,
     138.87762281450296,
     131.58664890288273,
     137.05327558190058,
     137.72578098691966,
     136.1238780857441,
     145.60425617813937,
     132.59136655488047,
     132.0193316660917,
     138.17523714822286,
     134.12596127113824,
     135.6810878942867,
     136.23481785505697,
     130.57293332629277,
     139.26552496139414,
     133.05012761159634,
     138.30430798682954,
     130.76973919701703,
     133.2647569268816,
     129.5507260993907,
     135.9554997039271,
     138.72296600609823,
     135.94231573760737,
     135.70644832737617,
     134.36472190558422,
     135.86653274026338,
     133.01890766771004,
     137.9382308523345,
     137.08063503384642,
     134.75971187845727,
     129.31411100302662,
     134.17252422345032,
     128.2094946496243,
     129.07109253828895,
     134.91794062258663,
     137.56092791083304,
     132.29492870389925,
     130.14000700057835,
     132.51651052126545,
     136.2790516179431,
     136.50272101210112,
     136.1741515154255,
     132.701845362704,
     131.9717824588997,
     130.39084548290163,
     134.37786569373995,
     135.207384795766,
     136.32233574806068,
     137.55294890799684,
     138.69534399048058,
     132.91921115580956,
     139.42983961916036,
     132.10866258441933,
     133.69674366503395,
     135.93632228488926,
     133.11573530784213,
     137.87668329295954,
     127.90822125546222,
     139.95069942844862,
     137.13674372877313,
     132.10734586007482,
     136.3366562557506,
     126.36645106268543,
     136.44704789773868,
     133.58588153681066,
     142.21144065327843,
     138.0216126187682,
     136.43053338077772,
     129.08886498031882,
     137.94402100684164,
     134.0986242345506,
     134.04216690104582,
     131.97259196727916,
     131.62913460082572,
     135.94756844485983,
     146.0363452890946,
     141.08202354991903,
     133.59468601505586,
     141.24537770043773,
     134.59247964676948,
     130.90842785555276,
     130.9341818737866,
     134.97696990152417,
     140.10822140640084,
     132.16409454681624,
     129.59062930989103,
     144.37125419895654,
     130.5305338938841,
     122.29125060428512,
     133.71501252523436,
     140.7257756059714,
     136.3771487243562,
     134.3728346023143,
     135.89419403408516,
     126.56064107946888,
     126.7055569201038,
     133.1100581571064,
     127.9019377420104,
     131.61183563498415,
     134.97315500400757,
     138.6006225095034,
     130.99937649697316,
     133.7808933495595,
     137.1000110663378,
     134.30507116554404,
     139.07835653521346,
     133.3048821641821,
     129.33088763598394,
     128.81445950842405,
     135.46168949618203,
     132.28842177531052,
     139.64734643241727,
     129.91695021461098,
     134.95353618374318,
     138.48190095427648,
     138.4464073000754,
     139.2243545497303,
     135.83248387963826,
     140.43057431758695,
     139.70201610087162,
     143.99876773496104,
     134.5517112818767,
     130.58582836076675,
     132.55640951384086,
     132.51149571500767,
     138.18900756742835,
     129.90350350079663,
     131.28916609123715,
     119.09618172906454,
     134.87741986259348,
     141.3300924547582,
     136.44719811563618,
     136.57937530943985,
     136.89511523646578,
     132.232280769603,
     135.76358290880825,
     127.3422527288784,
     135.76763204546117,
     136.55232574992579,
     135.25935653189188,
     129.82567877197766,
     148.10940410355764,
     133.5621911109665,
     135.80293919451097,
     134.69149129456963,
     130.80557884698035,
     135.9845339945226,
     136.84097383627767,
     137.0121833744881,
     128.7627074539561,
     135.27266668308502,
     129.97241367505458,
     123.25097450366674,
     132.132335473481,
     132.16435914163864,
     138.8924355857656,
     133.71095167849438,
     130.786983882348,
     133.63377562906052,
     140.54959979428756,
     135.35662396921924,
     129.83140471659883,
     136.35227400550676,
     140.80191674093572,
     135.44648155682827,
     131.84993759792755,
     127.45452873285572,
     130.6494090267367,
     137.54004933739256,
     136.12622651580145,
     130.35841354272776,
     138.61194830479093,
     130.09354400270394,
     132.9725082017072,
     135.79235316988203,
     136.04165100815985,
     132.3912177821114,
     136.57065086016613,
     136.25342544453633,
     147.09413652259497,
     135.15813748339852,
     132.62234403788665,
     126.54208351602689,
     129.2881634833256,
     131.90390690958142,
     131.6772044900074,
     139.82288432464549,
     135.22246739826755,
     144.7236720326942,
     133.2314820611611,
     139.80402813566158,
     140.46665774715814,
     135.5152777478594,
     129.08123888168393,
     127.08335034116315,
     136.66117699879172,
     135.6049868805449,
     136.5127558936456,
     135.59391649293232,
     134.03881091355532,
     137.47365219516752,
     138.35800021681243,
     143.65624890813626,
     134.68326004673685,
     133.06841075758751,
     142.30644099190602,
     131.4594401570824,
     131.85477751747524,
     142.56129957426273,
     138.7959630983813,
     143.10861364865252,
     123.87920554005159,
     138.6397883276342,
     130.742076841006,
     129.9480712772871,
     131.75947350335036,
     133.772393227429,
     131.44722768782964,
     135.27121103023757,
     127.9789635253643,
     131.24461791228796,
     134.6203225176201,
     132.64537516114302,
     138.48593938688936,
     135.64157909922392,
     138.62584256618678,
     127.57829528785372,
     140.77207782875425,
     135.67049326074766,
     130.51302746912899,
     139.63921079329214,
     138.82096698456436,
     138.7149881412255,
     139.05200691827008,
     133.07075257342584,
     140.02128927847198,
     132.009146876271,
     133.36998705144472,
     135.8685101332248,
     136.50190237044026,
     128.78609022349968,
     139.2086232477592,
     138.42519806474127,
     131.0421029802369,
     131.7301899240713,
     133.86971984551573,
     133.98796018660522,
     135.2278361386512,
     132.81553545933303,
     144.4818539390617,
     140.85583120182608,
     138.91166708541965,
     126.52349185610174,
     130.79825787081808,
     141.91571308287908,
     132.3621142449252,
     135.8333406590108,
     136.10394156409484,
     126.62055393046606,
     137.68523636973745,
     139.40642872272326,
     137.1955938132474,
     126.26463436748084,
     128.682704557519,
     137.3083508109959,
     136.66969280976156,
     136.18222099482261,
     138.35377095444395,
     126.01403324119501,
     133.41861489515082,
     124.24008484467358,
     129.9133922135339,
     136.94139213452934,
     134.50297042771933,
     136.36165826115368,
     128.32250494268203,
     133.6122617174307,
     126.4233881833026,
     137.29684552749032,
     132.43510120541043,
     138.20233274240954,
     133.44481578691997,
     135.91047597491195,
     124.8725338791585,
     128.7666433081478,
     136.75260193392944,
     128.65555108636818,
     135.66625538678682,
     135.3534115465572,
     140.4285873243591,
     142.02362850420374,
     127.44907521966977,
     133.1710886186229,
     127.05656702267213,
     135.39776952472312,
     129.1106421097435,
     143.35341181179353,
     133.99609288834878,
     122.73695610002744,
     131.9392289795895,
     136.83292648728386,
     136.5222960934844,
     127.9347699233719,
     128.84077769944776,
     133.51971450381555,
     128.76925639989167,
     133.1124818909506,
     135.85591690210876,
     135.5494470819913,
     130.93319856989743,
     134.33358854390394,
     134.81557975817447,
     141.8984588279584,
     137.78240416343453,
     132.60484687543803,
     131.11069066928962,
     136.95244311494272,
     130.46136481651652,
     127.576059620146,
     133.03018626872432,
     134.97454321557692,
     122.00474004515911,
     134.62565411984133,
     136.60843690485868,
     131.34606185658168,
     145.52170559488349,
     138.15264438341285,
     135.38841686995002,
     128.19828127618842,
     131.54750215546846,
     132.42169571081808,
     132.216672506366,
     133.6267285014799,
     136.18516463479892,
     129.04417753564803,
     134.42205228091404,
     130.47786472952825,
     131.63750193638214,
     137.5078853372789,
     131.19410783637133,
     136.726005508451,
     142.26906482817043,
     132.4140459819683,
     134.6780724368383,
     140.9026593555656,
     136.2716667978159,
     133.72402948348477,
     142.52473971336065,
     138.56015341986424,
     138.6393740351685,
     133.8317011795848,
     139.47379808932828,
     129.76712407882445,
     137.57429047769685,
     133.91549600852179,
     132.59831137964764,
     140.0774966652549,
     140.24792037592246,
     142.39931788588234,
     135.42791041382807,
     132.20429529948393,
     126.1240998013715,
     122.58673249005328,
     140.6200618568071,
     134.52335901894804,
     132.11746565852235,
     131.4829637769891,
     135.71192529273415,
     137.73577138419043,
     136.06745243251459,
     135.94188967307062,
     137.0705324695054,
     127.95926562849507,
     128.53800160513313,
     129.5204139699706,
     136.91649528017476,
     133.62314102482034,
     135.5578338219008,
     134.7440233645499,
     131.64404615157258,
     132.8413023359382,
     135.12979954841245,
     142.88498879939647,
     129.8249403160562,
     127.57413444602723,
     138.99323645819422,
     131.42251098652247,
     133.1678659226932,
     121.34780328953772,
     132.0731922642952,
     136.4814119677544,
     135.1470337730068,
     128.1609340414459,
     139.48096068243908,
     132.22202294711735,
     130.88346378147563,
     134.91438980018813,
     124.95160076747621,
     129.95686806204137,
     125.24092338266041,
     141.24921675891184,
     136.69110703317546,
     138.4426495958645,
     138.02529812310237,
     144.4290683477014,
     142.64816993487764,
     139.6666041098058,
     134.7436578369061,
     132.53711996265707,
     129.45836076627984,
     135.6247964272083,
     136.2432388862844,
     132.8803470515392,
     129.69765762698128,
     131.65766059838052,
     134.3712776380383,
     134.02680438293964,
     133.0593264648227,
     134.12379352650018,
     141.77195996492128,
     143.03684219427169,
     135.07935209061742,
     138.56552345671932,
     129.84507448826716,
     139.50927233373656,
     128.17196304143098,
     131.14238275133627,
     135.07632506261683,
     139.2554178310775,
     130.74010031064242,
     134.4069025915475,
     140.87111900965112,
     129.7474078253252,
     141.961573549611,
     139.29894026980725,
     143.57304922565444,
     136.20283284048915,
     140.0642630237586,
     138.506631672365,
     131.91731743223545,
     139.64848357251833,
     134.23959232468198,
     121.22823163888397,
     132.64977246584672,
     136.68114749173984,
     124.24114827690136,
     138.61737048217586,
     130.0481621707483,
     135.63689433945547,
     126.00574015073514,
     134.83253036812346,
     129.43028268223654,
     131.6241990266879,
     137.76201933226952,
     129.74427296692062,
     125.80961462638201,
     137.56547105611102,
     129.86973362746556,
     137.2221450504167,
     136.65763995062312,
     134.02767163974195,
     129.51278718496343,
     132.53089743857478,
     136.3201628140543,
     138.07173908141291,
     130.8896062799746,
     133.82164834257108,
     127.26686538774285,
     128.7883445565501,
     136.10179413809414,
     134.70771962647686,
     133.82435832373363,
     131.926469651889,
     137.1471960826258,
     128.36167057133247,
     128.15782125483435,
     132.33610285493296,
     127.54824468026587,
     132.41821757812815,
     133.42535621858923,
     137.22332364668097,
     133.53472835350084,
     132.88948747457127,
     141.38261665100654,
     142.56083087850277,
     133.03707505104884,
     138.88945502293382,
     136.38844562925914,
     130.10999449897258,
     131.9650025110834,
     135.23322210790886,
     131.98389812045386,
     135.9139471757918,
     134.54519477088226,
     126.6993147197969,
     136.92459178600026,
     137.17803969456529,
     135.41073403580162,
     129.9760242083077,
     138.61300847447205,
     128.66607268254268,
     132.1904498891318,
     139.78661951448282,
     140.54322711702991,
     129.23142189318983,
     138.5925755146701,
     132.1259293331799,
     127.96860412786656,
     138.9539699486678,
     135.30540579180905,
     131.61952312395914,
     139.22083687168143,
     139.47602449675333,
     131.8288186956396,
     124.98771581383022,
     132.76499590070603,
     137.79644683542494,
     131.19603526916657,
     138.2220096824923,
     136.56602740791925,
     132.92945651678858,
     129.8032059773272,
     132.90892446026314,
     133.44975958286886,
     147.12964475662844,
     135.28832370148143,
     128.29681515611753,
     136.94365161478743,
     133.85947665590612,
     132.95765273152506,
     136.3117414895533,
     142.73791099118037,
     136.5539538621281,
     142.15949627988806,
     128.51364073882368,
     139.3255026837532,
     135.11896652005424,
     129.90587655877752,
     140.48919339691835,
     143.64650740064062,
     125.57661602798161,
     138.54827523506043,
     133.57262826679033,
     135.8072798157492,
     131.7949550971851,
     138.17541236891623,
     128.89633244238175,
     133.50895389489378,
     137.6482622773241,
     134.6158288087855,
     132.47156530217765,
     140.69051079260004,
     127.6390049365225,
     133.39382295627462,
     131.1813122581282,
     132.45531958100878,
     131.86122739110212,
     131.98676084633132,
     133.37991200883638,
     132.47773021858737,
     130.65677071682242,
     144.23197137149924,
     133.3774913981006,
     139.1242024252893,
     132.70071794705865,
     136.4388701517642,
     138.04656320236992,
     133.74679922863655,
     130.95176347328996,
     135.10749785283392,
     139.4869875937905,
     128.28988293775492,
     134.5363787667753,
     131.57759175379007,
     132.83614704519172,
     135.87460525926997,
     131.7232994260579,
     136.49986648732792,
     134.6858011279651,
     144.70926166589473,
     138.70280942618507,
     143.0822918419198,
     135.79676379821595,
     132.80751503036083,
     134.1319434390563,
     131.85736309074193,
     144.95459059607194,
     137.964712079434,
     132.6777881048469,
     139.02576238193302,
     136.10311864487892,
     138.68620481499175,
     139.55575077449538,
     135.3024692862837,
     137.44788386642696,
     128.27720377971596,
     131.1040120447158,
     132.20448198384403,
     138.35691216711282,
     143.85787558668204,
     131.7681242767676,
     129.59330646579016,
     133.39138736963753,
     137.28959101804156,
     134.5713370387848,
     150.0]




```python
num_bins = 100
plt.figure(1)
plt.hist(u,num_bins, normed = 1.0, facecolor='green', alpha = 0.5)
plt.grid()
plt.show()
```


![png](output_22_0.png)
