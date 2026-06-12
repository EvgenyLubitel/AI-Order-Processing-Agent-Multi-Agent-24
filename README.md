# 🤖 AI Order Processing Agent + Битрикс24

Multi-Agent система на n8n для автоматической обработки заказов с интеграцией Битрикс24.

[![n8n](https://img.shields.io/badge/n8n-0.268.0-blue)](https://n8n.io)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT--3.5--Turbo-green)](https://openai.com)
[![Bitrix24](https://img.shields.io/badge/Bitrix24-REST_API-orange)](https://bitrix24.com)
[![License](https://img.shields.io/badge/license-MIT-yellow)](LICENSE)

---

## 📌 О проекте

**AI Order Processing Agent** — это мульти-агентная система для автоматической обработки заказов. Система анализирует запрос клиента, извлекает сущности, генерирует коммерческое предложение, обогащает ответ рекомендациями и **создаёт сделку в Битрикс24** через REST API.

**Ключевые возможности:**
- ✅ Извлечение клиента, товаров, количества, цен
- ✅ Генерация профессионального коммерческого предложения
- ✅ Рекомендации сопутствующих товаров
- ✅ Автоматическое создание сделки в Битрикс24
- ✅ Webhook API для интеграции

---

## 🏗️ Архитектура
Webhook → Main Orchestrator (AI Agent)
├── Entity Extractor (извлечение сущностей)
├── Offer Generator (генерация КП)
├── GraphRAG Enricher (рекомендации)
└── Bitrix24 Deal Creator (создание сделки)


---

## 🔧 Технологический стек

| Компонент | Технология |
|-----------|------------|
| Оркестрация | n8n |
| AI | OpenAI GPT (через AITUNNEL) |
| CRM | Битрикс24 REST API |
| Поиск/обогащение | GraphRAG |
| Интеграция | Webhook, HTTP Request |

---

## 🚀 Быстрый старт

### 1. Импорт workflow

Скачай `workflow.json` и импортируй в n8n.

### 2. Настройка переменных

| Переменная | Значение |
|------------|----------|
| `AITUNNEL_API_KEY` | Твой ключ AITUNNEL |
| `BITRIX24_WEBHOOK_URL` | URL вебхука Битрикс24 |

## 🧪 Тестирование

### PowerShell

```powershell
$body = @{
    message = "ООО Ромашка заказывает 10 ноутбуков ASUS ROG по 90000 руб"
} | ConvertTo-Json

$response = Invoke-RestMethod -Uri "https://n8n-graphrag-evgenylubitel.amvera.io/webhook-test/order-request" -Method POST -ContentType "application/json" -Body $body
$response.result
