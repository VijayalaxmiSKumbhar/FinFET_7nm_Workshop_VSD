# FinFET Circuit Design and Characterization

## Introduction

<details>
<summary> What is FinFET?</summary>
<br>
FINFET stands for Fin Field Effect Transistor it belongs to the FET family and it is a type of Multi gate MOSFET that is used in place of a common MOSFET.
  
#### Key Features of FinFET Technology
* `3D Structure:` The vertical fin design improves control over the channel, allowing for higher performance at smaller nodes.
* `Improved Electrostatic Control:` By surrounding the channel with the gate on three sides, FinFETs reduce leakage currents and improve switching speeds.
* `Scalability:` FinFET technology enables continued scaling of transistors beyond the limitations faced by planar designs.
</details>

<details>
<summary> Why FinFETs?</summary>
<br>
  
* To follow Moore’s, we have to increase the number of transistors which leads to downscaling of the transistor dimensions and results in several SCEs. 
* FinFET is one of the favorable devices due to more controllability of the gate over the channel 
* Chenming Hu, and his group in 1998 were the first who coined the term FinFET, as a result of the structure. 

<img width="975" height="481" alt="image" src="https://github.com/user-attachments/assets/c6bd333d-f849-4dc4-a326-d4c1928e0a00" />


</details>

<details>
<summary> nfet Characterization</summary>
<br>

## Schematic of nfet in Xschem

<img width="795" height="593" alt="image" src="https://github.com/user-attachments/assets/f62881df-5244-47a2-b7af-852a0397b87c" />


## nfet Spice Code
	
``` 
** sch_path: /home/vsduser/Desktop/nfetchar.sch
**.subckt nfetchar
Xnfet1 nfet_out nfet_in GND GND asap_7nm_nfet l=7e-009 nfin=14
R1 vdd nfet_out 1k m=1
V1 nfet_in GND 3
V2 VDD GND 3
**** begin user architecture code

 .dc v1 0 0.7 1m v2 0 0.7 0.2
.control
run
set xbrushwidth=3
let vd = vdd - nfet_out
let id  = vd/1000
plot id
.endc

**** end user architecture code
**.ends
.GLOBAL GND
.GLOBAL VDD
.GLOBAL nfet_in
**** begin user architecture code

.subckt asap_7nm_nfet S G D B l=7e-009 nfin=14
	nnmos_finfet S G D B BSIMCMG_osdi_N l=7e-009 nfin=14
.ends asap_7nm_nfet

.model BSIMCMG_osdi_N BSIMCMG_va (
+ TYPE = 1
************************************************************
*                         general                          *
************************************************************
+version = 107             bulkmod = 1               igcmod  = 1               igbmod  = 0
+gidlmod = 1               iimod   = 0               geomod  = 1               rdsmod  = 0
+rgatemod= 0               rgeomod = 0               shmod   = 0               nqsmod  = 0
+coremod = 0               cgeomod = 0               capmod  = 0               tnom    = 25
+eot     = 1e-009          eotbox  = 1.4e-007        eotacc  = 1e-010          tfin    = 6.5e-009
+toxp    = 2.1e-009        nbody   = 1e+022          phig    = 4.2466          epsrox  = 3.9
+epsrsub = 11.9            easub   = 4.05            ni0sub  = 1.1e+016        bg0sub  = 1.17
+nc0sub  = 2.86e+025       nsd     = 2e+026          ngate   = 0               nseg    = 5
+l       = 2.1e-008        xl      = 1e-009          lint    = -2e-009         dlc     = 0
+dlbin   = 0               hfin    = 3.2e-008        deltaw  = 0               deltawcv= 0
+sdterm  = 0               epsrsp  = 3.9             nfin    = 1
+toxg    = 1.80e-009
************************************************************
*                            dc                            *
************************************************************
+cit     = 0               cdsc    = 0.01            cdscd   = 0.01            dvt0    = 0.05
+dvt1    = 0.47            phin    = 0.05            eta0    = 0.07            dsub    = 0.35
+k1rsce  = 0               lpe0    = 0               dvtshift= 0               qmfactor= 2.5
+etaqm   = 0.54            qm0     = 0.001           pqm     = 0.66            u0      = 0.0303
+etamob  = 2               up      = 0               ua      = 0.55            eu      = 1.2
+ud      = 0               ucs     = 1               rdswmin = 0               rdsw    = 200
+wr      = 1               rswmin  = 0               rdwmin  = 0               rshs    = 0
+rshd    = 0               vsat    = 70000           deltavsat= 0.2             ksativ  = 2
+mexp    = 4               ptwg    = 30              pclm    = 0.05            pclmg   = 0
+pdibl1  = 0               pdibl2  = 0.002           drout   = 1               pvag    = 0
+fpitch  = 2.7e-008        rth0    = 0.225           cth0    = 1.243e-006      wth0    = 2.6e-007
+lcdscd  = 5e-005          lcdscdr = 5e-005          lrdsw   = 0.2             lvsat   = 0
************************************************************
*                         leakage                          *
************************************************************
+aigc    = 0.014           bigc    = 0.005           cigc    = 0.25            dlcigs  = 1e-009
+dlcigd  = 1e-009          aigs    = 0.0115          aigd    = 0.0115          bigs    = 0.00332
+bigd    = 0.00332         cigs    = 0.35            cigd    = 0.35            poxedge = 1.1
+agidl   = 1e-012          agisl   = 1e-012          bgidl   = 10000000        bgisl   = 10000000
+egidl   = 0.35            egisl   = 0.35
************************************************************
*                            rf                            *
************************************************************
************************************************************
*                         junction                         *
************************************************************
************************************************************
*                       capacitance                        *
************************************************************
+cfs     = 0               cfd     = 0               cgso    = 1.6e-010        cgdo    = 1.6e-010
+cgsl    = 0               cgdl    = 0               ckappas = 0.6             ckappad = 0.6
+cgbo    = 0               cgbl    = 0
************************************************************
*                       temperature                        *
************************************************************
+tbgasub = 0.000473        tbgbsub = 636             kt1     = 0               kt1l    = 0
+ute     = -0.7            utl     = 0               ua1     = 0.001032        ud1     = 0
+ucste   = -0.004775       at      = 0.001           ptwgt   = 0.004           tmexp   = 0
+prt     = 0               tgidl   = -0.007          igt     = 2.5
************************************************************
*                          noise                           *
************************************************************
**)
.control
pre_osdi /home/vsduser/Downloads/bsimcmg.osdi
.endc


**** end user architecture code
.end 
```

` plot id `

<img width="792" height="600" alt="image" src="https://github.com/user-attachments/assets/991b4816-4b63-45f5-91d4-3aea95bd2a51" />

` plot id vs vd `

<img width="796" height="600" alt="image" src="https://github.com/user-attachments/assets/62d706fb-b4d8-46ac-8ded-56a90169a8c4" />


</details>

<details>
<summary> FinFET Inverter Characteristics </summary>
<br>

` Inverter Schematic in Xschem `

<img width="797" height="675" alt="image" src="https://github.com/user-attachments/assets/a3440b4f-37f6-46e5-87b5-ec2daafdeaf2" />

</details>
