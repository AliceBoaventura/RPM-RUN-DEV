#!/bin/bash

# Verifica se um arquivo foi passado como argumento
if [ -z "$1" ]; then
  echo "Uso: $0 arquivo.rpm"
  exit 1
fi

ARQUIVO_RPM="$1"

# Verifica se o arquivo existe
if [ ! -f "$ARQUIVO_RPM" ]; then
  echo "Erro: Arquivo '$ARQUIVO_RPM' não encontrado."
  exit 2
fi

# Verifica se é root
if [ "$(id -u)" -ne 0 ]; then
  echo "Este script precisa ser executado como root (use sudo)."
  exit 3
fi

# Detecta se dnf ou yum está instalado
if command -v dnf >/dev/null 2>&1; then
  echo "Instalando com dnf..."
  dnf install -y "$ARQUIVO_RPM"
elif command -v yum >/dev/null 2>&1; then
  echo "Instalando com yum..."
  yum install -y "$ARQUIVO_RPM"
elif command -v rpm >/dev/null 2>&1; then
  echo "Instalando com rpm (sem resolver dependências)..."
  rpm -ivh "$ARQUIVO_RPM"
else
  echo "Nenhum gerenciador de pacotes rpm (dnf/yum/rpm) encontrado."
  exit 4
fi
