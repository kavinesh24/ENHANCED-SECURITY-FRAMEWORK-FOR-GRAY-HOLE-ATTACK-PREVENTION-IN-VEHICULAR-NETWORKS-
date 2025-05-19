SIMULATION 
puts "Enter option Leach (0) or Lightweight (1) or comp (2)" 
set opt_ [gets stdin] 
set bopt_ 1 
if {$opt_==0} { 
set bopt_ 0 
} 
if {$opt_==2} { 
exec xgraph en_grp_0 en_grp_1 -x "time" -y "energy" -lw 2 & 
exec xgraph PDF_0 PDF_1 -x "time s" -y "pkts" -lw 2 & 
#exec xgraph TPDF_0 TPDF_1 TPDF_2 -x "time s" -y "pkts" -nl 
bar -brw 0.5 & 
exec xgraph OH_0 OH_1 -x "time s" -y "pkts" -lw 2 & 
exec xgraph delay_0 delay_1 -x "tech" -y "Delay rate" -bg "black" 
fg "white" -bar -brw 1 -nl & 
exec xgraph th_0 th_1 -x "time" -y "Packet size" -t "Throughput" 
bg "black" -fg "white" -lw 3 & 
exit 
} 
# 
====================================================
 ================== 
# Define options 
# 
====================================================
 ================== 
set val(chan) Channel/Wireless Channel; # Channel Type 
65 
set val(prop) Propagation/TwoRayGround ;#Nakagami 
#TwoRayGround; # radio-propagation model 
set val(netif) Phy/WirelessPhy 
set val(ant)Antenna/Omni Antenna; # antenna model 
set val(mac) Mac/802_11 
set val(ll) LL; # link layer type 
set val(rp) DSDV; # AODV; # routing protocol 
set val(ifq) Queue/DropTail/PriQueue; #; #; CMUPriQueue; # #   
Queue/DropTail/PriQueue for AODV & DSDV CMUPriQueue for DSR  
set val(ifqlen) 50; # max packet in ifq 
set val(nn) 51; # number of mobilenodes 
set val(x) 500; 
set val(y) 500; 
#Set val(nam) out.nam; 
#Set val(traffic) ftp; # cbr/poisson/ftp 
# 
====================================================
 ======================== 
set ns_  
[new Simulator] 
set ns $ns_ 
set ran [new RNG]; #random number generator 
set tracefd [open out.tr w] 
set namtrace[open out.nam w] 
set En_fl[open en_grp_$opt_ w] 
$ns_ namtrace-all-wireless $namtrace $val(x) $val(y) 
$ns_ trace-all $tracefd 
set topo [new Topography] 
$topo load_flatgrid $val(x) $val(y) 
set God[create-god100] 
66 
# 
====================================================
 ========================= 
if {1} { 
set txp 0.001 
$ns_ node-config -energyModel EnergyModel \ -rxPower 0.0005 \ -txPower $txp \ -initialEnergy 100 \ -idlePower 0.5 
} 
# 
====================================================
 ==================== 
$ns_ node-config -adhocRouting $val(rp) \ -llType $val(ll) \ -macType $val(mac)\ -ifqType $val(ifq) \ -ifqLen $val(ifqlen) \ -antType $val(ant) \ -propType $val(prop) \ -phyType $val(netif) \ -channelType  $val(chan)\ -topoInstance $topo \ -agentTrace ON \ -routerTrace ON \ -macTrace ON \ -movementTrace ON  
67 
# 
============================================ 
$ns_ color 1 red 
$ns_ color 2 green 
$ns_ color 3 purple 
# 
========================================== 
source trace 
source Lightweight.tcl 
source Leach.tcl 
set fg 300 
set PS [new Pan_Sim] 
for {set i 0} {$i<$val(nn)} {incr i} { 
set node_($i) [$ns_ node] 
set nd_($i) [$PS Node] 
set CH_lst [list] 
$node_($i) color black 
} 
$node_ (0) set X_ 83 
$node_ (0) set Y_ 168 
$node_ (1) set X_ 59 
$node_ (1) set Y_ 110 
$node_ (2) set X_ 100 
$node_ (2) set Y_ 13 
$node_ (3) set X_ 120 
$node_ (3) set Y_ 100 
$node_ (4) set X_ 140 
$node_ (4) set Y_ 160 
$node_ (5) set X_ 155 
68 
$node_ (5) set Y_ 270 
$node_ (5) set X_ 1 
$node_ (5) set Y_ 270 
set y 200 
set z 100 
set n 6 
#$ns_ at 7.1 "$nd_(1) make-failure" 
for {set i 200} {$i<280} {incr i +70} { 
for {set j 100} {$j<180} {incr j +70} { 
$node_($n) set X_ $i 
$node_($n) set Y_ $j 
incr n 
if {$n >=$val(nn)} {break} 
} 
} 
if {$n >=$val(nn)} {break} 
$node_ (10) set X_ 237 
$node_ (10) set Y_ 134 
$node_ (11) set X_ 165 
$node_ (11) set Y_ 280 
$node_ (11) set X_ -25.4646 
$node_ (11) set Y_ 473.608 
set in 12 
for {set i 310} {$i<390} {incr i +70} { 
for {set j 250} {$j<330} {incr j +70} { 
$node_($n) set X_ $i 
$node_($n) set Y_ $j 
incr n 
if {$n >=$val(nn)} {break} 
69 
} 
if {$n >=$val(nn)} {break} 
} 
$node_ (16) set X_ 344 
$node_ (16) set Y_ 290 
$node_ (17) set X_ 100 
$node_ (17) set Y_ 399 
$node_ (18) set X_ 170 
$node_ (18) set Y_ 402 
$node_ (19) set X_ 100 
$node _ (19) set Y_ 481 
$node_ (20) set X_ 170 
$node_ (20) set Y_ 481 
$node_ (21) set X_ 135 
$node_ (21) set Y_ 446 
$node_ (22) set X_ -87.9252 
$node_ (22) set Y_ 425.696 
$node_ (23) set X_ -58.3266 
$node_ (23) set Y_ 444.847 
$node_ (24) set X_ -106.207 
$node_ (24) set Y_ 442.236 
$node_ (25) set X_ -55.715 
$node_ (25) set Y_ 420.472 
$node_ (26) set X_ 194.132 
$node_ (26) set Y_ 237.658 
$node_ (27) set X_ 242.883 
$node_ (27) set Y_ 245.493 
$node_ (28) set X_ 221.119 
70 
$node_ (28) set Y_ 268.128 
$node_ (29) set X_ 279.446 
$node_ (29) set Y_ 237.659 
$node_ (30) set X_ 266.387 
$node_ (30) set Y_ 270.74 
$node_ (31) set X_ 227.213 
$node_ (31) set Y_ 329.066 
$node_ (32) set X_ 208.061 
$node_ (32) set Y_ 310.784 
$node_ (33) set X_ 181.944 
$node_ (33) set Y_ 321.23 
$node_ (34) set X_ 151.475 
$node_ (34) set Y_ 346.476 
$node_ (35) set X_ 152.455 
$node_ (35) set Y_ 305.017 
$node_ (36) set X_ -52.8857 
$node_ (36) set Y_ 137.329 
$node_ (37) set X_ -29.2721 
$node_ (37) set Y_ 190.32 
$node_ (38) set X_ -75.5199 
$node_ (38) set Y_ 161.921 
$node_ (39) set X_ -24.7018 
$node_ (39) set Y_ 163.336 
$node_ (40) set X_ -63.6587 
$node_ (40) set Y_ 189.561 
$node_ (41) set X_ -110.124 
$node_ (41) set Y_ 248.432 
71 
$node_ (42) set X_ -161.813 
$node_ (42) set Y_ 260.619 
$node_ (43) set X_ -122.856 
$node_ (43) set Y_ 200.225 
$node_ (44) set X_ -178.244 
$node_ (44) set Y_ 229.824 
$node_ (45) set X_ -148.102 
$node_ (45) set Y_ 228.736 
$node_ (46) set X_ -102.289 
$node_ (46) set Y_ 299.794 
$node_ (47) set X_ -69.6437 
$node_ (47) set Y_ 350.504 
$node_ (48) set X_ -113.171 
$node_ (48) set Y_ 356.924 
$node_ (49) set X_ -160.724 
$node_ (49) set Y_ 326.019  
$node_ (50) set X_ -117.85 
$node_ (50) set Y_ 324.082 
$nd_ (0) set-en 70 
$nd_ (7) set-en 70 
$nd_ (0) set drt_ 0.015 
$nd_ (1) set drt_ 0.018 
$nd_ (1) set drt_ 0.021 
$nd_ (6) set drt_ 0.014 
$nd_ (7) set drt_ 0.018 
$nd_ (8) set drt_ 0.022 
set BS 5 
#$ns_ at 1.0 "$nd_ (5) label BaseStation" 
$ns_ at 0 "$node_ (5) label BS" 
$ns_ at 0 "$node_ (5) color red" 
72 
#$ns_ initial_node_pos $node_ (5) 30 
#Set Mc 11 
$ns_ at 1.1 "$nd_ (0) send_Data $BS" 
$ns_ at 1.11 "$nd_ (1) send_Data $BS" 
$ns_ at 1.12 "$nd_ (2) send_Data $BS" 
$ns_ at 1.13 "$nd_ (3) send_Data $BS" 
$ns_ at 1.14 "$nd_ (4) send_Data $BS" 
$ns_ at 1.1 "$nd_ (6) send_Data $BS" 
$ns_ at 1.11 "$nd_ (7) send_Data $BS" 
$ns_ at 1.12 "$nd_ (8) send_Data $BS" 
$ns_ at 1.13 "$nd_ (9) send_Data $BS" 
$ns_ at 1.14 "$nd_ (10) send_Data $BS" 
$ns_ at 1.1 "$nd_ (16) send_Data $BS" 
$ns_ at 1.11 "$nd_(12) send_Data $BS" 
$ns_ at 1.12 "$nd_ (13) send_Data $BS" 
$ns_ at 1.13 "$nd_(14) send_Data $BS" 
$ns_ at 1.14 "$nd_(15) send_Data $BS" 
$ns_ at 1.1 "$nd_(21) send_Data $BS" 
$ns_ at 1.11 "$nd_(17) send_Data $BS" 
$ns_ at 1.12 "$nd_(18) send_Data $BS" 
$ns_ at 1.13 "$nd_(19) send_Data $BS" 
$ns_ at 1.14 "$nd_(20) send_Data $BS" 
$ns_ at 1.1 "$nd_(22) send_Data $BS" 
$ns_ at 1.11 "$nd_(23) send_Data $BS" 
$ns_ at 1.12 "$nd_(24) send_Data $BS" 
$ns_ at 1.13 "$nd_(25) send_Data $BS" 
$ns_ at 1.13 "$nd_(11) send_Data $BS" 
$ns_ at 1.1 "$nd_(26) send_Data $BS" 
$ns_ at 1.11 "$nd_(27) send_Data $BS" 
73 
$ns_ at 1.12 "$nd_(28) send_Data $BS" 
$ns_ at 1.13 "$nd_(29) send_Data $BS" 
$ns_ at 1.14 "$nd_(30) send_Data $BS" 
$ns_ at 1.1 "$nd_(31) send_Data $BS" 
$ns_ at 1.11 "$nd_(32) send_Data $BS" 
$ns_ at 1.12 "$nd_(33) send_Data $BS" 
$ns_ at 1.13 "$nd_(34) send_Data $BS" 
$ns_ at 1.14 "$nd_(35) send_Data $BS" 
$ns_ at 1.1 "$nd_(36) send_Data $BS" 
$ns_ at 1.11 "$nd_(37) send_Data $BS" 
$ns_ at 1.12 "$nd_(38) send_Data $BS" 
$ns_ at 1.13 "$nd_(39) send_Data $BS" 
$ns_ at 1.14 "$nd_(40) send_Data $BS" 
$ns_ at 1.1 "$nd_(41) send_Data $BS" 
$ns_ at 1.11 "$nd_(42) send_Data $BS" 
$ns_ at 1.12 "$nd_(43) send_Data $BS" 
$ns_ at 1.13 "$nd_(44) send_Data $BS" 
$ns_ at 1.14 "$nd_(45) send_Data $BS" 
$ns_ at 1.1 "$nd_(46) send_Data $BS" 
$ns_ at 1.11 "$nd_(47) send_Data $BS" 
$ns_ at 1.12 "$nd_(48) send_Data $BS" 
$ns_ at 1.13 "$nd_(49) send_Data $BS" 
$ns_ at 1.14 "$nd_(50) send_Data $BS" 
if {$opt_>0} { 
$ns_ at 1.3 "$nd_(6) make-failure" 
} else { 
$ns_ at 1.3 "$nd_(8) make-failure" 
$ns_ at 1.3 "$nd_(50) make-failure" 
$ns_ at 1.3 "$nd_(33) make-failure" 
74 
} 
proc Grph {} { 
global En_fl nd_ ns_ 
set en 100 
set nd x 
foreach n [array names nd_] { 
set ene [$nd_($n) set energy] 
if {$en>$ene && ($n!=5 && $n!=11) && $ene>2} {  
set en $ene 
set nd $n 
} 
}  
puts "$nd -- $en" 
puts $En_fl "[$ns_ now] $en" 
$ns_ at [expr [$ns_ now]+1] "Grph" 
}  
$ns_ at 0 "Grph" 
for {set i 0} {$i<$val(nn)} {incr i} { 
$ns_ initial_node_pos $node_($i) 10 
} 
proc finish {} { 
global ns_ namtrace  nd_ opt_ En_fl 
$ns_ flush-trace 
close $namtrace 
close $En_fl 
exec awk -f pdf.awk out.tr >PDF_$opt_ 
exec awk -f OH.awk out.tr >OH_$opt_ 
exec awk -f th.awk out.tr >th_$opt_ 
#exec awk -f LT.awk out.tr >LifeTime_$opt_ 
75 
#exec awk -f energy.awk out.tr >en_grp_$opt_ 
exec nam out.nam & 
#exec xgraph en_grp_$opt_ -x "time" -y "energy" -lw 2 & 
exec xgraph th_$opt_ -x "time s" -y "pkts" & 
exec xgraph PDF_$opt_ -x "time s" -y "pkts" & 
exec xgraph OH_$opt_ -x "time s" -y "pkts" & 
#exec xgraph LifeTime_$opt_ -x "No of Rounds" -y "No of Active 
Nodes" &   
exit 
} 
$ns_ at 40 "finish" 
$ns_ run
