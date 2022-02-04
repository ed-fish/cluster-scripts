#!/bin/bash
machines=( coppola campion bigelow hitchcock welles lavacore)

if [ $# -ge 1 ]
then
    while getopts m: flag
        do
            case "${flag}" in
            m) machine=${OPTARG};;
            h) echo "-m str machine-name";;
            *) echo "bad arg, use '-m machine-name'";;
        esac
    done
    ssh "$USER"@"$machine" nvidia-smi --query-gpu=name,memory.free,utilization.memory --format=csv
else
    for i in "${machines[@]}"
    do 
        echo "MACHINE: $i"
        read -p "View GPU availability for $i?" yn
        case $yn in
            [Yy]* ) ssh "$USER"@"$i" nvidia-smi --query-gpu=name,memory.free,utilization.memory --format=csv;;
            [Nn]* ) continue;;
            * ) echo "Select yes or no";;
        esac
    done
fi