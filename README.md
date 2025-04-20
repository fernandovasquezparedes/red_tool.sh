#!/bin/bash

function escanear_puertos() {
    read -p "Ingresa la IP o dominio: " objetivo
    sudo nmap -p- "$objetivo"
}

function escanear_equipos() {
    read -p "Ingresa el rango de red (ej. 192.168.1.0/24): " red
    sudo nmap -sn "$red"
}

function verificar_so() {
    read -p "Ingresa la IP o dominio: " objetivo
    sudo nmap -O "$objetivo"
}

function realizar_dos() {
    read -p "Ingresa la IP objetivo: " ip
    echo "Iniciando ataque ICMP (10 paquetes por ronda). Presiona Ctrl+C para detener..."
    while true; do
        ping -c 10 "$ip"
        sleep 1
    done
}

function verificar_ip() {
    echo "Tu IP interna es: $(hostname -I)"
    echo "Tu IP pública es: $(curl -s ifconfig.me)"
}

function salir() {
    echo "Saliendo del script. ¡Hasta luego!"
    exit 0
}

while true; do
    clear
    echo "===== MENU DE HERRAMIENTAS DE RED ====="
    echo "1. Escanear Puertos"
    echo "2. Escanear Equipos"
    echo "3. Verificar Sistema Operativo"
    echo "4. Realizar DoS (10 ICMP por ronda)"
    echo "5. Verificar IP"
    echo "6. Salir"
    echo "======================================="
    read -p "Elige una opción [1-6]: " opcion

    case $opcion in
        1) escanear_puertos ;;
        2) escanear_equipos ;;
        3) verificar_so ;;
        4) realizar_dos ;;
        5) verificar_ip ;;
        6) salir ;;
        *) echo "Opción inválida. Intenta de nuevo." ;;
    esac

    read -p "Presiona [Enter] para continuar..."
done
