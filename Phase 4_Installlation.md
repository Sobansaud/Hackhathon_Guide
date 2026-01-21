`# 🚀 Hackathon 2 – Phase IV

## DevOps & Kubernetes Tools Installation Guide

This document is **COMPLETED** and ready to use for **Hackathon 2 – Phase IV**.  
Follow this guide to install all required tools on **Windows**.

---

## ⚠️ Important Instructions

- Use **Windows OS**
- Run installer file **as Administrator**
- Restart terminal/system if required

---

## 📦 Tools Included

- Docker Desktop  
- Chocolatey  
- kubectl  
- Helm  
- Minikube  
- kubectl-ai (via Krew)

---

## 🛠️ Phase IV Installer Script

### Step 1: Like And Subscribe My Channel


# CodeVerse Soban


### Step 2: Step By Step Installation All Packages

```bat
@echo off
title Phase IV Tools Installer - Hackathon 2
echo.
echo ==============================================
echo   Hackathon 2 - Phase IV Tools Installer
echo   (Docker, Chocolatey, kubectl, Helm, Minikube, kubectl-ai)
echo   Run as Administrator!
echo ==============================================
echo.

echo [1/7] Checking if running as Administrator...
net session >nul 2>&1
if %errorLevel% neq 0 (
    echo ERROR: Please run this file as Administrator!
    pause
    exit /b
)

echo [2/7] Installing Chocolatey...
if (-not (Get-Command choco -ErrorAction SilentlyContinue)) {
    Write-Host "Chocolatey not found - Installing now..."
    Set-ExecutionPolicy Bypass -Scope Process -Force
    [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072
    iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
    Write-Host "Chocolatey installed! Restart PowerShell to use choco."
} else {
    Write-Host "Chocolatey already installed. Version:"
    choco --version
}

echo [3/7] Docker Desktop (Manual)
echo Download from:
echo https://www.docker.com/products/docker-desktop
pause

echo [4/7] Installing kubectl...
choco install kubernetes-cli -y

echo [5/7] Installing Helm...
choco install kubernetes-helm -y

echo [6/7] Installing Minikube...
choco install minikube -y

echo [7/7] Installing kubectl-ai...
powershell -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://raw.githubusercontent.com/kubernetes-sigs/krew/master/krew.ps1'))"
set PATH=%PATH%;%USERPROFILE%\.krew\bin
kubectl krew install ai

echo Installation Complete!
pause
```

---

## ✅ Verify Installation

Run these commands:

```bash
docker --version
choco --version
kubectl version --client
helm version
minikube version
kubectl ai --help
```

---

## ▶️ Start Minikube

```bash
minikube start --driver=docker
```

---

## 🎯 Status

✅ **Phase IV Completed Successfully**

---

## ❤️ Support

If this helped you:

**Subscribe CodeVerse**  
📺 YouTube: CodeVerse by Soban  
🔔 Like • Share • Subscribe  

#CodeVerse #Hackathon2 #DevOps #Kubernetes
