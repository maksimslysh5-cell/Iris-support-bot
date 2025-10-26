# Iris-support-bot
Support Bot!
# -*- coding: utf-8 -*-
import telebot
from telebot import types
import sqlite3
import os

# Если ты запускаешь бота на Railway — токен можно хранить в переменной окружения
TOKEN = os.getenv("TOKEN", "ВАШ_ТОКЕН_ТУТ")
bot = telebot.TeleBot(TOKEN)

# Создание базы данных (SQLite)
conn = sqlite3.connect("iris_bot.db", check_same_thread=False)
cursor = conn.cursor()

# Таблицы
cursor.execute("""
CREATE TABLE IF NOT EXISTS users (
    id INTEGER PRIMARY KEY,
    balance INTEGER DEFAULT 0,
    vip BOOLEAN DEFAULT 0,
    rank INTEGER DEFAULT 1,
    warns INTEGER DEFAULT 0,
    muted BOOLEAN DEFAULT 0
)
""")

cursor.execute("""
CREATE TABLE IF NOT EXISTS rewards (
    user_id INTEGER,
    reward_text TEXT
)
""")

cursor.execute("""
CREATE TABLE IF NOT EXISTS notes (
    user