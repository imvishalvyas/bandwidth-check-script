### 1.netpps.sh
 
```
#!/bin/bash

INTERVAL="1"  # update interval in seconds

if [ -z "$1" ]; then

        echo

        echo usage: $0 [network-interface]

        echo

        echo e.g. $0 eth0

        echo

        echo shows packets-per-second

        exit

fi

IF=$1

while true

do

        R1=`cat /sys/class/net/$1/statistics/rx_packets`

        T1=`cat /sys/class/net/$1/statistics/tx_packets`

        sleep $INTERVAL

        R2=`cat /sys/class/net/$1/statistics/rx_packets`

        T2=`cat /sys/class/net/$1/statistics/tx_packets`

        TXPPS=`expr $T2 - $T1`

        RXPPS=`expr $R2 - $R1`

        echo "TX $1: $TXPPS pkts/s RX $1: $RXPPS pkts/s"

done
```

# Measure Network Bandwidth on an Interface

### 2.netpps.sh

 
```
#!/bin/bash

INTERVAL="1"  # update interval in seconds

if [ -z "$1" ]; then

        echo

        echo usage: $0 [network-interface]

        echo

        echo e.g. $0 eth0

        echo

        exit

fi

IF=$1

while true

do

        R1=`cat /sys/class/net/$1/statistics/rx_bytes`

        T1=`cat /sys/class/net/$1/statistics/tx_bytes`

        sleep $INTERVAL

        R2=`cat /sys/class/net/$1/statistics/rx_bytes`

        T2=`cat /sys/class/net/$1/statistics/tx_bytes`

        TBPS=`expr $T2 - $T1`

        RBPS=`expr $R2 - $R1`

        TKBPS=`expr $TBPS / 1024`

        RKBPS=`expr $RBPS / 1024`

        echo "TX $1: $TKBPS kb/s RX $1: $RKBPS kb/s"

done
```


The following screenshot shows the above two scripts in action.
