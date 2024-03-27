'''voise, chat, message, text, photo, document'''
import csv
import requests
from datetime import datetime
from telebot import types
import telebot
import time
import os

import datetime as dt
from datetime import datetime

now = datetime.now()
hour = now.strftime("%H")
minute = now.strftime("%M")
year = now.strftime("%Y")
month = now.strftime("%m")
day = now.strftime("%d")

last_day = now.day-1
next_day = now.day+1
last_day = str(last_day)
next_day = str(next_day)




# #time1 = dt.now()
# day = dt.datetime.now().day
# month = dt.datetime.now().month
# year = dt.datetime.now().year


result = time.localtime(time.time())
Token = ''
bot = telebot.TeleBot('')
my_chat_id: int= 5899535945
evmenkov = 1892740912
psFEP = -4109016649
test_group_chat = -1002108034889
URL = 'https://api.telegram.org/bot'
name_1 = "ANNA"
seconds = time.time()










# 1. выбор проведение чек листа или отправка отчета

@bot.message_handler(commands=['start'])
def repeat(message: telebot.types.Message):
    text=('Выберите: кнопака chek_list - это по проверкам, а кнопка shift_report для отправки отчета: \n /chek_list\n /shift_report')
    bot.send_message(message.chat.id, text)

# 2. если в п.1 выбрано то выбираеться позиция проведения проверки т.е. чек листа
@bot.message_handler(commands=['chek_list'])
def chek_list(message):
    text = ('Выберите необходимые позиции для проверки: \n /WIS \n /texture \n /PECVD \n /PVD \n /Metallization \n /fotootdjik \n /CIS \n /pasta')
    bot.send_message(message.chat.id, text)



# 3. если в п.1 выбрано отправка отчета, то проверяеться условие по критерии по отправке отчета
@bot.message_handler(commands=['shift_report'])
def shift_report(message):
    if result.tm_hour >= 7 and result.tm_hour < 8:
        keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)
        button_phone = types.KeyboardButton(text="Отчет ночной смены")
        button_geo = types.KeyboardButton(text="отчет отправлю позже, но не позже 08:00")
        keyboard.add(button_phone, button_geo)
        bot.send_message(message.chat.id, "Выберите позиции: (кнопка-отправить_отчет)"
                                          " или (кнопка-отчет отправлю чуть позже)", reply_markup=keyboard)



    elif result.tm_hour >= 8 and result.tm_hour < 22:
        keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)
        button_phone = types.KeyboardButton(text="Отчет дневной смены")
        button_geo = types.KeyboardButton(text="отчет отправлю позже, но не позже 20:00")
        keyboard.add(button_phone, button_geo)
        bot.send_message(message.chat.id, "Выберите позиции: (кнопка-отправить_отчет)"
                                          " или (кнопка-отчет отправлю чуть позже,  но не позже 20:00)", reply_markup=keyboard)


    else:
        bot.send_message(message.chat.id, 'Братан тормози! сейчас не время для отправки отчета. '
                                          'Отчет необходимо отправлять с 07:00 до 08:00 (если ты сегодня работаешь в ночной смене) или с 19:00 до 20:00 (если ты сегодня работаешь в дневной смене.)')




@bot.message_handler(commands=['WIS'])
def WIS(message):
    text = ('Выберите необходимые позиции для проверки в зоне WIS:  \n /Check_clining_in_zone_WIS \n /Compressed_Air_WIS \n /Electrical_WIS')
    bot.send_message(message.chat.id, text)


@bot.message_handler(commands=['Check_clining_in_zone_WIS'])
def WIS1(message):

    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства
    button_phone = types.KeyboardButton(text="Да чисто в зоне WIS")
    button_geo = types.KeyboardButton(text="Нет не чисто в зоне WIS")
    keyboard.add(button_phone, button_geo)
    bot.send_message(message.chat.id, "Чисто ли в зоне WIS? Что означает чисто: а) между оборудованиями отсутствует строительный мусор "
                                      "б) отсутствует пакеты, бутылки в) не востребованные предметы убраны в зону хранения", reply_markup=keyboard)


@bot.message_handler(commands=['Compressed_Air_WIS'])
def WIS2(message):
    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства
    button_phone = types.KeyboardButton(text="В зоне WIS ЕСТЬ звук травления воздуха")
    button_geo = types.KeyboardButton(text="В зоне WIS НЕТ звук травления воздуха")
    keyboard.add(button_phone, button_geo)
    bot.send_message(message.chat.id, "В зоне WIS присутствует ли свисятщие или сипящие звуки (звук травления сжатого воздуха) от сжатого воздуха? ", reply_markup=keyboard)


@bot.message_handler(commands=['Electrical_WIS'])
def WIS3(message):
    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства
    button_phone = types.KeyboardButton(text="Кабель/эле-ика нарушена на WIS")
    button_geo = types.KeyboardButton(text="Кабель/эле-ика НЕ нарушена на WIS")
    keyboard.add(button_phone, button_geo)
    bot.send_message(message.chat.id, "В зоне WIS присутствует ли (нарушение кабеля и узлов электроники) наличие запаха оплавления изоляции провода, визуально видно ли искры от проводов, слышно ли звук от искр проводов? ", reply_markup=keyboard)



@bot.message_handler(commands=['texture'])
def texture(message):
    text = ('Выберите необходимые позиции для проверки в зоне Текстурирования: \n /Check_leaks_DI_water_in_zone_texture \n /Check_leaks_cooling_water_in_zone_texture \n /Check_clining_in_zone_texture \n /Compressed_Air_texture \n /Electrical_texture')
    bot.send_message(message.chat.id, text)



# 5. если в п.2 выбрано по проверке установка texture
@bot.message_handler(commands=['Check_leaks_DI_water_in_zone_texture'])

def texture1(message):
    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства
    button_phone = types.KeyboardButton(text="YES_2")
    button_geo = types.KeyboardButton(text="NO_2")
    keyboard.add(button_phone, button_geo)
    bot.send_message(message.chat.id, "Есть ли утечки DI воды на текстурирование как на магистрали до оборудования и во внутренней системе технологического оборудования", reply_markup=keyboard)


@bot.message_handler(commands=['Check_leaks_cooling_water_in_zone_texture'])
def texture2(message):
    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства
    button_phone = types.KeyboardButton(text="Есть течь охлаждающей воды на Текстурировании")
    button_geo = types.KeyboardButton(text="Нет течи охлаждающей воды на Текстурировании")
    keyboard.add(button_phone, button_geo)
    bot.send_message(message.chat.id, "Есть ли утечки охлаждающей воды на текстурирование как на магистрали до оборудования и во внутренней системе технологического оборудования", reply_markup=keyboard)



@bot.message_handler(commands=['Check_clining_in_zone_texture'])
def texture3(message):
    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства
    button_phone = types.KeyboardButton(text="Да чисто в зоне Текстурирования")
    button_geo = types.KeyboardButton(text="Нет не чисто в зоне Текстурирования")
    keyboard.add(button_phone, button_geo)
    bot.send_message(message.chat.id, "Чисто ли в зоне Текстурирования? Что озночает чисто: а) между оборудованиями отсутствует строительный мусор "
                                      "б) отсутствует пакеты, бутылки в) не востребованные предметы убраны в зону хранения", reply_markup=keyboard)


@bot.message_handler(commands=['Compressed_Air_texture'])
def texture4(message):

    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства
    button_phone = types.KeyboardButton(text="Есть звук травления воздуха зоне Текст-ия")
    button_geo = types.KeyboardButton(text="Нет звука травления воздуха зоне Текст-ия")
    keyboard.add(button_phone, button_geo)
    bot.send_message(message.chat.id, "В зоне Текстурирования присутствует ли свисятщие или сипящие звуки (звук травления сжатого воздуха) от сжатого воздуха? ", reply_markup=keyboard)


@bot.message_handler(commands=['Electrical_texture'])
def texture5(message):
    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства
    button_phone = types.KeyboardButton(text="Кабель/эле-ика нарушена на текстурировании")
    button_geo = types.KeyboardButton(text="Кабель/эле-ика НЕ нарушена на текстурировании")
    keyboard.add(button_phone, button_geo)
    bot.send_message(message.chat.id, "В зоне Текстурирования присутствует ли (нарушение кабелей и узлов электроники) наличие запаха оплавления изоляции провода, визуально видно ли искры от проводов, слышно ли звук от искр проводов? ", reply_markup=keyboard)



@bot.message_handler(commands=['PECVD'])
def pecvd(message):
    text = ('Выберите необходимые позиции для проверки в зоне Фотоотджига: \n /Check_leaks_colling_water_in_zone_PECVD \n /Check_leaks_drains_in_zone_PECVD \n /Check_clining_in_zone_PECVD \n /Compressed_Air_PECVD \n /Electrical_PECVD')
    bot.send_message(message.chat.id, text)



@bot.message_handler(commands=['Check_leaks_colling_water_in_zone_PECVD'])
def pecvd1(message):
    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства
    button_phone = types.KeyboardButton(text="Да_4")
    button_geo = types.KeyboardButton(text="Нет_4")
    keyboard.add(button_phone, button_geo)
    bot.send_message(message.chat.id, "Есть ли утечки охлаждающей воды на оборудованиях PECVD", reply_markup=keyboard)


@bot.message_handler(commands=['Check_clining_in_zone_PECVD'])
def pecvd2(message):
    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства
    button_phone = types.KeyboardButton(text="Да чисто в зоне PECVD")
    button_geo = types.KeyboardButton(text="Не чисто в зоне PECVD")
    keyboard.add(button_phone, button_geo)
    bot.send_message(message.chat.id, " Чисто ли в зоне PECVD? Что озночает чисто: а) между оборудованиями отсутствует строительный мусор "
                                      "б) отсутствует пакеты, бутылки в) не востребованные предметы убраны в зону хранения" , reply_markup=keyboard)



@bot.message_handler(commands=['Compressed_Air_PECVD'])
def pecvd3(message):

    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства
    button_phone = types.KeyboardButton(text="Есть звук травления в зоне PECVD")
    button_geo = types.KeyboardButton(text="Нет звука травления в зоне PECVD")
    keyboard.add(button_phone, button_geo)
    bot.send_message(message.chat.id, "В зоне PECVD присутствует ли свисятщие или сипящие звуки (звук травления сжатого воздуха)?", reply_markup=keyboard)


@bot.message_handler(commands=['Electrical_PECVD'])
def pecvd4(message):
    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства
    button_phone = types.KeyboardButton(text="Кабель/эле-ика нарушена на PECVD")
    button_geo = types.KeyboardButton(text="Кабель/эле-ика НЕ нарушена на PECVD")
    keyboard.add(button_phone, button_geo)
    bot.send_message(message.chat.id, "В зоне PECVD присутствует ли (нарушение кабеля и узлов электроники) наличие запаха оплавления изоляции провода, визуально видно ли искры от проводов, слышно ли звук от искр проводов?", reply_markup=keyboard)



@bot.message_handler(commands=['Check_leaks_drains_in_zone_PECVD'])
def pecvd5(message):
    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства
    button_phone = types.KeyboardButton(text="Есть утечки стоков на PECVD")
    button_geo = types.KeyboardButton(text="Отсутствует утечки стоков на PECVD")
    keyboard.add(button_phone, button_geo)
    bot.send_message(message.chat.id, "Есть ли утечки стоков от PECVD в зоне PECVD", reply_markup=keyboard)


@bot.message_handler(commands=['PVD'])
def PVD1(message):
    text = ('Выберите необходимые позиции для проверки в зоне PVD: \n /Check_leaks_colling_water_in_zone_PVD \n /Check_clining_in_zone_PVD \n /Compressed_Air_PVD \n /Electrical_PVD ')
    bot.send_message(message.chat.id, text)


@bot.message_handler(commands=['Check_leaks_colling_water_in_zone_PVD'])
def pvd2(message):
    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства
    button_phone = types.KeyboardButton(text="Да_5")
    button_geo = types.KeyboardButton(text="Нет_5")
    keyboard.add(button_phone, button_geo)
    bot.send_message(message.chat.id, "Есть ли утечки охлаждающей воды на оборудованиях PVD", reply_markup=keyboard)



@bot.message_handler(commands=['Check_clining_in_zone_PVD'])
def pvd3(message):
    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства
    button_phone = types.KeyboardButton(text="Да чисто в зоне PVD")
    button_geo = types.KeyboardButton(text="Не чисто в зоне PVD")
    keyboard.add(button_phone, button_geo)
    bot.send_message(message.chat.id, " Чисто ли в зоне PVD? Что озночает чисто: а) между оборудованиями отсутствует строительный мусор "
                                      "б) отсутствует пакеты, бутылки в) не востребованные предметы убраны в зону хранения", reply_markup=keyboard)


@bot.message_handler(commands=['Compressed_Air_PVD'])
def pvd4(message):
    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства
    button_phone = types.KeyboardButton(text="Есть звук травления на PVD")
    button_geo = types.KeyboardButton(text="Нет звука травления на PVD")
    keyboard.add(button_phone, button_geo)
    bot.send_message(message.chat.id, "В зоне PVD присутствует ли свистящие или сипящие звуки (звук травления сжатого воздуха)?", reply_markup=keyboard)

@bot.message_handler(commands=['Electrical_PVD'])
def pvd5(message):
    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства
    button_phone = types.KeyboardButton(text="Кабель/эле-ика нарушена на PVD")
    button_geo = types.KeyboardButton(text="Кабель/эле-ика НЕ нарушена на PVD")
    keyboard.add(button_phone, button_geo)
    bot.send_message(message.chat.id, "В зоне PVD присутствует ли (нарушение кабеля и узлов электроники) наличие запаха оплавления изоляции провода, визуально видно ли искры от проводов, слышно ли звук от искр проводов?", reply_markup=keyboard)



@bot.message_handler(commands=['Metallization'])
def Metallization(message):
    text = ('Выберите необходимые позиции для проверки в зоне Металлизации: \n /Check_leaks_colling_water_in_zone_Metallization \n /Check_clining_in_zone_Metallization \n /Compressed_Air_Metallization \n /Electrical_Metallization')
    bot.send_message(message.chat.id, text)


@bot.message_handler(commands=['Check_leaks_colling_water_in_zone_Metallization'])
def Metallization1(message):
    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства
    button_phone = types.KeyboardButton(text="Есть течь охлаждающей воды на Металлизации")
    button_geo = types.KeyboardButton(text="Нет течи охлаждающей воды на Металлизации")
    keyboard.add(button_phone, button_geo)
    bot.send_message(message.chat.id, "Есть ли утечки охлаждающей воды на Металлизации? ", reply_markup=keyboard)



@bot.message_handler(commands=['Check_clining_in_zone_Metallization'])
def Metallization2(message):
    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства
    button_phone = types.KeyboardButton(text="Да чисто в зоне Металлизации")
    button_geo = types.KeyboardButton(text="Нет не чисто в зоне Металлизации")
    keyboard.add(button_phone, button_geo)
    bot.send_message(message.chat.id, "Чисто ли в зоне Металлизации? Что означает чисто: а) между оборудованиями отсутствует строительный мусор "
                                      "б) отсутствует пакеты, бутылки в) не востребованные предметы убраны в зону хранения", reply_markup=keyboard)


@bot.message_handler(commands=['Compressed_Air_Metallization'])
def Metallization3(message):
    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства
    button_phone = types.KeyboardButton(text="Есть звук травления на Металлизации")
    button_geo = types.KeyboardButton(text="Нет звука травления на Металлизации")
    keyboard.add(button_phone, button_geo)
    bot.send_message(message.chat.id, "В зоне Металлизации присутствует ли свисятщие или сипящие звуки (звук травления сжатого воздуха)?", reply_markup=keyboard)


@bot.message_handler(commands=['Electrical_Metallization'])
def Metallization4(message):
    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства
    button_phone = types.KeyboardButton(text="Кабель/эле-ика нарушена на Металлизации")
    button_geo = types.KeyboardButton(text="Кабель/эле-ика НЕ нарушена на Металлизации")
    keyboard.add(button_phone, button_geo)
    bot.send_message(message.chat.id, "В зоне Металлизации присутствует ли (нарушение кабелей и узлов электроники) наличие запаха оплавления изоляции провода, визуально видно ли искры от проводов, слышно ли звук от искр проводов?", reply_markup=keyboard)



# 4. если в п.2 выбрано по проверке установка fotootdjik

@bot.message_handler(commands=['fotootdjik'])
def fotootdjik1(message):
    text = ('Выберите необходимые позиции для проверки в зоне Фотоотджига: \n /Check_leaks_colling_water_in_zone_Fotootgig \n /Check_clining_in_zone_Fotootgig \n /Compressed_Air_Fotootgig \n /Electrical_Fotootgig')
    bot.send_message(message.chat.id, text)


@bot.message_handler(commands=['Check_leaks_colling_water_in_zone_Fotootgig'])
def fotootdjik2(message):

    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства
    button_phone = types.KeyboardButton(text="YES_1")
    button_geo = types.KeyboardButton(text="NO_1")
    keyboard.add(button_phone, button_geo)
    bot.send_message(message.chat.id, "Есть ли утечки охлаждающей воды на фотоотджиге? ", reply_markup=keyboard)



@bot.message_handler(commands=['Check_clining_in_zone_Fotootgig'])
def fotootdjik3(message):
    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства
    button_phone = types.KeyboardButton(text="Да чисто в зоне фотоотджига")
    button_geo = types.KeyboardButton(text="Нет не чисто в зоне Фотоотджига")
    keyboard.add(button_phone, button_geo)
    bot.send_message(message.chat.id, "Чисто ли в зоне фотоотджига? Что озночает чисто: а) между оборудованиями отсутствует строительный мусор "
                                      "б) отсутствует пакеты, бутылки в) не востребованные предметы убраны в зону хранения", reply_markup=keyboard)

@bot.message_handler(commands=['Compressed_Air_Fotootgig'])
def fotootdjik4(message):
    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства
    button_phone = types.KeyboardButton(text="Есть звук травления на Фотоотджиге")
    button_geo = types.KeyboardButton(text="Нет звука травления на Фотоотджиге")
    keyboard.add(button_phone, button_geo)
    bot.send_message(message.chat.id, "В зоне Фотоотджига присутствует ли свисятщие или сипящие звуки (звук травления сжатого воздуха)?", reply_markup=keyboard)


@bot.message_handler(commands=['Electrical_Fotootgig'])
def fotootdjik5(message):
    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства

    button_phone = types.KeyboardButton(text="Кабель/эле-ика нарушена на Фотоотджиге")
    button_geo = types.KeyboardButton(text="Кабель/эле-ика НЕ нарушена на Фотоотджиге")
    keyboard.add(button_phone, button_geo)
    bot.send_message(message.chat.id, "В зоне Фотоотджига присутствует ли (нарушение кабеля и узлов электроники) наличие запаха оплавления изоляции провода, визуально видно ли искры от проводов, слышно ли звук от искр проводов?", reply_markup=keyboard)



@bot.message_handler(commands=['CIS'])
def CIS(message):
    text = ('Выберите необходимые позиции для проверки в зоне Металлизации: \n /Check_clining_in_zone_CIS \n /Compressed_Air_CIS \n /Electrical_CIS')
    bot.send_message(message.chat.id, text)



@bot.message_handler(commands=['Check_clining_in_zone_CIS'])
def CIS2(message):
    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства
    button_phone = types.KeyboardButton(text="Да чисто в зоне CIS")
    button_geo = types.KeyboardButton(text="Нет не чисто в зоне CIS")
    keyboard.add(button_phone, button_geo)
    bot.send_message(message.chat.id, "Чисто ли в зоне CIS? Что означает чисто: а) между оборудованиями отсутствует строительный мусор "
                                      "б) отсутствует пакеты, бутылки в) не востребованные предметы убраны в зону хранения", reply_markup=keyboard)


@bot.message_handler(commands=['Compressed_Air_CIS'])
def CIS3(message):
    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства
    button_phone = types.KeyboardButton(text="Есть звук травления воздуха в зоне CIS")
    button_geo = types.KeyboardButton(text="Нет звука травления воздуха в зоне CIS")
    keyboard.add(button_phone, button_geo)
    bot.send_message(message.chat.id, "В зоне Фотоотджига присутствует ли свисятщие или сипящие звуки (звук травления сжатого воздуха)?", reply_markup=keyboard)


@bot.message_handler(commands=['Electrical_CIS'])
def CIS4(message):
    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства
    button_phone = types.KeyboardButton(text="Кабель нарушен в зоне CIS")
    button_geo = types.KeyboardButton(text="Кабель НЕ нарушен в зоне CIS")
    keyboard.add(button_phone, button_geo)
    bot.send_message(message.chat.id, "В зоне CIS присутствует ли (нарушение кабеля и узлов электроники) наличие запаха оплавления изоляции провода, визуально видно ли искры от проводов, слышно ли звук от искр проводов?", reply_markup=keyboard)





# 6. если в п.2 выбрано по проверке пасты
@bot.message_handler(commands=['pasta'])
def pasta(message):
    text = ('Выберите: кнопку fridge_№1-это Холодильник_№1; кнопку fridge_№2-это Холодильник_№2; кнопку box - это паста в коробке. '
            ' \n /fridge1 \n /fridge2 \n /box')
    bot.send_message(message.chat.id, text)


# 7. если в п.6 выбрано по проверке холодильника №1
@bot.message_handler(commands=['fridge1'])
def fridge1(message):
    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства
    button_phone = types.KeyboardButton(text="Да_1")
    button_geo = types.KeyboardButton(text="Нет_1")
    button_geo1 = types.KeyboardButton(text="Не работает 1")
    keyboard.add(button_phone, button_geo, button_geo1)
    bot.send_message(message.chat.id, "Температура в холодильнике №1 от -18 гр до -21? или холодильник не работет?", reply_markup=keyboard)


# 8. если в п.6 выбрано по проверке холодильника №2
@bot.message_handler(commands=['fridge2'])
def fridge2(message):
    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства
    button_phone = types.KeyboardButton(text="Да_2")
    button_geo = types.KeyboardButton(text="Нет_2")
    button_geo1 = types.KeyboardButton(text="Не работает 2")
    keyboard.add(button_phone, button_geo, button_geo1)
    bot.send_message(message.chat.id, "Температура в холодильнике №2 от -18 гр до -21? или холодильник не работет?", reply_markup=keyboard)

# 9. если в п.9 выбрано по проверке пасты
@bot.message_handler(commands=['box'])
def box(message):
    keyboard = types.ReplyKeyboardMarkup(row_width=2, one_time_keyboard=True)  # клавиатура автомтически меняеться в зависимости от устройства
    button_phone = types.KeyboardButton(text="Да 3")
    button_geo = types.KeyboardButton(text="Нет 3")
    keyboard.add(button_phone, button_geo)
    bot.send_message(message.chat.id, "Пломба на ящике в целости?", reply_markup=keyboard)




# 10. выполняються различные сценарии исходящих от блоков 3, 4, 5, 7, 8, 9

@bot.message_handler(content_types=['text'])
def several(message):
# Дневная смена________________________
    seconds = time.time()
    now = datetime.now()
    hour = now.strftime("%H")
    minute = now.strftime("%M")
    # 10.1 отправка отчета

    if result.tm_hour >= 8 and result.tm_hour < 20:
        if message.text == "Отчет дневной смены":

            w = open("Проверка инженерии на WIS " + day + "." + month + "." + year + ".csv", "rb")
            requests.get(f'{URL}{Token}/sendDocument', data={'chat_id': psFEP}, files={'document': w})


            f = open("Проверка пасты " + day + "." + month + "." + year + ".csv", "rb")
            requests.get(f'{URL}{Token}/sendDocument', data={'chat_id': psFEP}, files={'document': f})

            m = open("Проверка инженерии на Текстурировании " + day + "." + month + "." + year + ".csv", "rb")
            requests.get(f'{URL}{Token}/sendDocument', data={'chat_id': test_group_chat}, files={'document': m})

            t = open("Проверка инженерии на Текстурировании " + day + "." + month + "." + year + ".csv", "rb")
            requests.get(f'{URL}{Token}/sendDocument', data={'chat_id': test_group_chat}, files={'document': t})

            z = open("Проверка инженерии на PECVD " + day + "." + month + "." + year + ".csv", "rb")
            requests.get(f'{URL}{Token}/sendDocument', data={'chat_id': test_group_chat}, files={'document': z})

            v = open("Проверка инженерии на PVD " + day + "." + month + "." + year + ".csv", "rb")
            requests.get(f'{URL}{Token}/sendDocument', data={'chat_id': test_group_chat}, files={'document': v})

            n = open("Проверка инженерии на Металлизации " + day + "." + month + "." + year + ".csv", "rb")
            requests.get(f'{URL}{Token}/sendDocument', data={'chat_id': test_group_chat}, files={'document': n})

            l = open("Проверка инженерии на Фотоотджиге " + day + "." + month + "." + year + ".csv", "rb")
            requests.get(f'{URL}{Token}/sendDocument', data={'chat_id': test_group_chat}, files={'document': l})

            d = open("Проверка инженерии на CIS " + day + "." + month + "." + year + ".csv", "rb")
            requests.get(f'{URL}{Token}/sendDocument', data={'chat_id': test_group_chat}, files={'document': d})

            с = open("Проверка чистоты в зоне оборудований " + day + "." + month + "." + year + ".csv", "rb")
            requests.get(f'{URL}{Token}/sendDocument', data={'chat_id': test_group_chat}, files={'document': с})




            bot.send_message(message.chat.id, 'Отчет дневной смены в '+ hour+':'+ minute +  ' отправлен')


        # 10.2 фиксирование результатов пломбы на ящике, когда она целая
        elif message.text == 'Да 3':

            with open("Проверка пасты " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Пломба на ящике с пастой целая, которая принята ПС ФЭП")
                )
            file.close()
            bot.reply_to(message, ' Зафиксировано в  '+ hour+':'+ minute +  ', что пломба на ящике (на балансе ПС ФЭП) целая')




        # 10.3 фиксирование результатов пломбы на ящике, когда она НЕ целая
        elif message.text == 'Нет 3':

            with open("Проверка пасты " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Пломба на ящике с пастой НЕ целая, которая принята ПС ФЭП")
                )
            file.close()
            bot.reply_to(message, ' Зафиксировано в  '+ hour+':'+ minute +  ', что пломба на ящике НЕ целая, которая принята ПС ФЭП')


        # 10.4 результаты проверки холодильника №1, когда она не работает
        elif message.text == 'Не работает 1':

            with open("Проверка пасты " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Обнаружено, что холодильник №1 НЕ работает")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано в  '+ hour+':'+ minute +  ', что холодильник №1 не работает. \nНеобходимо сделать следующее согласно Операционной Карте:\n'
                         '\n1. Если также 2-ой холодильник не работает, необходимо вызвать электриков и подключить дизель генератор.\n'
                         '\n2. Если только 1-ый холодильник не работает, необходимо пасту переставить с 1-ого холодильника на 2-ой холодильник.\n'
                         '\n3. Если только 1-ый холодильник не работает и паста не влезает в 2-ой холодильник, то необходимо перенести '
                         'пасту в 3-ий холодильник, для включения 3-го холодильника необходимо вызвать электрика ')



        # 10.5 результаты проверки холодильника №1, когда она находиться в требуемом диапазоне температуры
        elif message.text == 'Да_1':
            with open("Проверка пасты " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В холодильнике №1 температура находиться в диапазоне от -18 гр до -21 гр")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано в  '+ hour+':'+ minute +  ', что в холодильнике температура находиться в диапазоне от -18 гр до -21 гр')

        # 10.6 результаты проверки холодильника №1, когда она находиться НЕ требуемом диапазоне температуры
        elif message.text == 'Нет_1':
            with open("Проверка пасты " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), "В холодильнике №1 температура НЕ находиться в диапазоне от -18 гр до -21 гр")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано в  '+ hour+':'+ minute +  ', что в холодильнике температура не находиться в диапазоне от -18 гр до -21 гр\n'
                         '\nНеобходимо сделать следующее согласно Операционной Карте:\n'
                         '\n1. Если температура выше -16 гр но ниже -15 гр то сделать следующее:\n'
                         '\n 1.1 Мониторить температуру в течении 10 минут, если температура не отпускаеться, то необходимо перенести пасту с'
                         '       с холодильника №1 в холодильник №2 (это только в том случае если у холодильника №2 температуара'
                         '       находиться в диапазоне от -18 гр до -21 гр)\n '
                         '\n2. Если температура выше -15 градусов, то перенести пасту с холодильника №1 в холодильник №2\n'
                         '\n3. Если температура выше -15 градусов и если нет мест в холодильнике №2 то пасту перенести 3-ий холодильник')




        # 10.7 результаты проверки холодильника №1, когда она НЕ работает
        elif message.text == 'Не работает 2':
            with open("Проверка пасты " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Обнаружено, что холодильник №2 НЕ работает")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано  '+ hour+':'+ minute +  ', что холодильник №2 не работает. \nНеобходимо сделать следующее согласно Операционной Карте:\n'
                         '\n1. Если также 1-ый холодильник не работает, необходимо вызвать электриков и подключить дизель генератор.\n'
                         '\n2. Если только 1-ый холодильник не работает, необходимо пасту переставить с 1-ого холодильника на 2-ой холодильник.\n'
                         '\n3. Если только 1-ый холодильник не работает и паста не влезает в 2-ой холодильник, то необходимо перенести '
                         'пасту в 3-ий холодильник, для включения 3-го холодильника необходимо вызвать электрика ')

        # 10.8 результаты проверки холодильника №1, когда температура находиться в требуемом дипазоне
        elif message.text == 'Да_2':
            with open("Проверка пасты " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В холодильнике №2 температура находиться в диапазоне от -18 гр до -21 гр")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано в  '+ hour+':'+ minute +  ', что в холодильнике №2 температура находиться в диапазоне от -18 гр до -21 гр')

        # 10.9 результаты проверки холодильника №1, когда температура находиться в НЕ требуемом дипазоне
        elif message.text == 'Нет_2':
            with open("Проверка пасты " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), "В холодильнике №2 температура НЕ находиться в диапазоне от -18 гр до -21 гр")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано в  '+ hour+':'+ minute +  ', что в холодильнике №2 температура не находиться в диапазоне от -18 гр до -21 гр\n'
                         '\nНеобходимо сделать следующее согласно Операционной Карте:\n'
                         '\n1. Если температура выше -16 гр но ниже -15 гр то сделать следующее:\n'
                         '\n 1.1 Мониторить температуру в течении 10 минут, если температура не отпускаеться, то необходимо перенести пасту с'
                         '       с холодильника №2 в холодильник №1 (это только в том случае если у холодильника №1 температуара'
                         '       находиться в диапазоне от -18 гр до -21 гр)\n '
                         '\n2. Если температура выше -15 градусов, то перенести пасту с холодильника №2 в холодильник №1\n'
                         '\n3. Если температура выше -15 градусов и если нет мест в холодильнике №1 то пасту перенести 3-ий холодильник')




        elif message.text == 'Нет 3':
            with open("Проверка пасты " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Зафиксировано, что пломба на ящике не целая")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано в  '+ hour+':'+ minute +  ', что Пломба не цела. Необходимо:'
                                                                             '\n1. Фотографировать сорванную пломбу.'
                                                                             '\n2. Фотографировать содержимое ящика.'
                                                                             '\n3. Произвести подсчет количества банок внутри ящика'
                                                                             '\n4. Сообщить начальника ПС ФЭП')


        elif message.text == 'Да 3':
            with open("Проверка пасты " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Зафиксировано, что пломба на ящике целая")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано в  '+ hour+':'+ minute +  ', что пломба целая на ящике')




        elif message.text == 'В зоне WIS ЕСТЬ звук травления воздуха':
            with open("Проверка инженерии на WIS " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне WIS обнаружено звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне WIS есть звук травления воздуха. \n1. Сообщить ССО, '
        
                                                                                           'если травление воздуха происходит внутри оборудования. \n2. Сообщить дежурному от инженерной службы и сообщить ССО, если травление воздуха происходит в магистральной линии (до оборудования).   ')



        elif message.text == "В зоне WIS НЕТ звук травления воздуха":

            with open("Проверка инженерии на WIS " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне WIS отсутствует звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время '+ hour+':'+ minute +  ' в зоне WIS отсутствует травление воздуха')



        elif message.text == 'Кабель/эле-ика нарушена на WIS':
            with open("Проверка инженерии на WIS " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне WIS обнаружено повреждение электроники и/или кабеля  ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне WIS обнаружено повреждение электроники и/или кабеля. \n1. Сообщить ССО, '
    
                                                                                           'если повреждение внутри оборудования. \n2. Сообщить дежурному электрику от инженерной службы и сообщить ССО, если повреждение находиться вне оборудования (до оборудования).   ')


        elif message.text == "Кабель/эле-ика НЕ нарушена на WIS":

            with open("Проверка инженерии на WIS " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне WIS отсутствует повреждение электроники и/или кабеля ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время '+ hour+':'+ minute +  ' в зоне WIS отсутствует повреждение электроники и/или кабеля')




        elif message.text == 'Нет не чисто в зоне WIS':
            with open("Проверка чистоты в зоне оборудований " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне PVD НЕ чисто ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне WIS НЕ чисто. Требуется'                                         
                                                                                           ' организовать уборку мусора. ')



        elif message.text == "Да чисто в зоне WIS":

            with open("Проверка чистоты в зоне оборудований " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне WIS чисто ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время '+ hour+':'+ minute +  ' в зоне WIS чисто')





        elif message.text == 'Да чисто в зоне Текстурирования':

            with open("Проверка чистоты в зоне оборудований " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Текстурирования чисто ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время '+ hour+':'+ minute +  ' в зоне Текстурирования чисто')



        elif message.text == 'Нет не чисто в зоне Текстурирования':

            with open("Проверка чистоты в зоне оборудований " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Текстурирования НЕ чисто ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время '+ hour+':'+ minute +  ' в зоне Текстурирования НЕ чисто. Требуется'
                                                                                        ' организовать уборку мусора. ')




        elif message.text == 'Есть звук травления воздуха зоне Текст-ия':
            with open("Проверка инженерии на Текстурировании " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Текстурирования обнаружено звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Текстурирования есть звук травления воздуха. \n1. Сообщить ССО, '

                                                                                           'если травление воздуха происходит внутри оборудования. \n2. Сообщить дежурному от инженерной службы и сообщить ССО, если травление воздуха происходит в магистральной линии (до оборудования).   ')



        elif message.text == "Нет звука травления воздуха зоне Текст-ия":
            with open("Проверка инженерии на Текстурировании " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Текстурирования отсутствует звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время '+ hour+':'+ minute +  ' в зоне Текстурирования отсутствует травление воздуха')



        elif message.text == 'Кабель/эле-ика нарушена на текстурировании':
            with open("Проверка инженерии на Текстурировании " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Текстурировании обнаружено повреждение электроники и/или кабеля  ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Текстурирования обнаружено повреждение электроники и/или кабеля. \n1. Сообщить ССО, '
    
                                                                                           'если повреждение внутри оборудования. \n2. Сообщить дежурному электрику от инженерной службы и сообщить ССО, если повреждение находиться вне оборудования (до оборудования).   ')


        elif message.text == "Кабель/эле-ика НЕ нарушена на текстурировании":

            with open("Проверка инженерии на Текстурировании " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Текстурирования отсутствует повреждение электроники и/или кабеля ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Текстурирования отсутствует повреждение электроники и/или кабеля')

            # 10.12 результаты проверки Текстурированя, когда течь воды обнаружено



        elif message.text == 'YES_2':
            with open("Проверка инженерии на Текстурировании " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка DI воды в зоне Текстурирования обнаружено ")
                )
            file.close()

            bot.reply_to(message,'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Текстурирования обнаружено утечки DI воды:'
                                                                                                   '\n1. Сообщить ССО если утечка DI воды находиться внутри оборудования и закрыть запорную арматуру'
                                                                                                   '\n2. Cообщить ССО и инженерную службу если утчека DI воды находиться в магистрали до технологического оборудования ' )


        # 10.13 результаты проверки Текстурированя, когда течь воды отсутсвует
        elif message.text == 'NO_2':
            with open("Проверка инженерии на Текстурировании " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка DI воды в зоне Текстурирования отсутствует")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано в  ' + hour + ':' + minute + ' по отсутствию утечек DI воды в зоне Текстурирования ')





        elif message.text == 'Есть течь охлаждающей воды на Текстурировании':
            with open("Проверка инженерии на Текстурировании " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка охлаждающей воды в зоне Текстурирования обнаружено ")
                )
            file.close()

            bot.reply_to(message,'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Текстурирования обнаружено утечки охлаждающей воды:'
                                                                                                   '\n1. Сообщить ССО, если утечка охлаждающей воды находиться внутри оборудования и закрыть запорную арматуру'
                                                                                                   '\n2. Cообщить ССО и инженерную службу, если утчека охлаждающей воды находиться в магистрали до технологического оборудования ' )


        # 10.13 результаты проверки Текстурированя, когда течь воды отсутсвует
        elif message.text == 'Нет течи охлаждающей воды на Текстурировании':
            with open("Проверка инженерии на Текстурировании " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка охлаждающей воды в зоне Текстурирования отсутствует")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано в  ' + hour + ':' + minute + ' по отсутствию утечек охлаждающей воды в зоне Текстурирования ')






        elif message.text == 'Да_4':
            with open("Проверка инженерии на PECVD " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка охлаждающей воды в зоне PECVD обнаружено ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PECVD обнаружено утечки охлаждающей воды:'
                                                                                           '\n1. Сообщить ССО, если утечка охлаждающей воды находиться внутри оборудования и закрыть запорную арматуру'
                                                                                           '\n2. Cообщить ССО и инженерную службу, если утчека охлаждающей воды находиться в магистрали до технологического оборудования ')



        elif message.text == 'Нет_4':
            with open("Проверка инженерии на PECVD " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка охлаждающей воды в зоне PECVD ОТСУТСВУЕТ ")
                )
            file.close()
            bot.reply_to(message, ' Информация зафиксировано в  '+ hour+':'+ minute +  ' по отсутствию утечек охлаждающей воды на оборудованиях PECVD ')




        elif message.text == 'Есть утечки стоков на PECVD':
            with open("Проверка инженерии на PECVD " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечки стоков на PECVD обнаружено ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PECVD обнаружено утечки стоков:'
                                                                                           '\n Cообщить ССО и инженерную службу, касаемо наличии утечки стоков')



        elif message.text == 'Отсутствует утечки стоков на PECVD':
            with open("Проверка инженерии на PECVD " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка стоков в зоне PECVD ОТСУТСВУЕТ ")
                )
            file.close()
            bot.reply_to(message, ' Информация зафиксировано в  '+ hour+':'+ minute +  ' по отсутствию утечек стоков в зоне PECVD ')




        elif message.text == "Да чисто в зоне PECVD":

            with open("Проверка чистоты в зоне оборудований " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне PECVD чисто ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PECVD чисто')


        elif message.text == 'Не чисто в зоне PECVD':

            with open("Проверка чистоты в зоне оборудований " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне PECVD НЕ чисто ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PECVD НЕ чисто. Требуеться организовать уборку мусора. ')




        elif message.text == 'Кабель/эле-ика нарушена на PECVD':
            with open("Проверка инженерии на PECVD " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне PECVD обнаружено повреждение электроники и/или кабеля  ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PECVD обнаружено повреждение электроники и/или кабеля. \n1. Сообщить ССО, '

                                                                                           'если повреждение внутри оборудования. \n2. Сообщить дежурному электрику от инженерной службы и сообщить ССО, если повреждение находиться вне оборудования (до оборудования).   ')



        elif message.text == "Кабель/эле-ика НЕ нарушена на PECVD":

            with open("Проверка инженерии на PECVD " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне PECVD отсутствует повреждение электроники и/или кабеля ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PECVD отсутствует повреждение электроники и/или кабеля')



        elif message.text == 'Есть звук травления в зоне PECVD':
            with open("Проверка инженерии на PECVD " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне PECVD обнаружено звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PECVD есть звук травления воздуха. \n1. Сообщить ССО, '

                                                                                           'если травление воздуха происходит внутри оборудования. \n2. Сообщить дежурному от инженерной службы и сообщить ССО, если травление воздуха происходит в магистральной линии (до оборудования).   ')



        elif message.text == "Нет звука травления в зоне PECVD":
            with open("Проверка инженерии на PECVD " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне PECVD отсутствует звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время '+ hour+':'+ minute +  ' в зоне PECVD отсутствует травление воздуха')





        elif message.text == "Да чисто в зоне PVD":

            with open("Проверка чистоты в зоне оборудований " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне PVD чисто ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время '+ hour+':'+ minute +  ' в зоне PVD чисто')




        elif message.text == 'Не чисто в зоне PVD':
            with open("Проверка чистоты в зоне оборудований " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне PVD НЕ чисто ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PVD НЕ чисто. Требуется'                                         
                                                                                           ' организовать уборку мусора. ')



        elif message.text == 'Да_5':
            with open("Проверка инженерии на PVD " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка охлаждающей воды в зоне PVD обнаружено ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PVD обнаружено утечки охлаждающей воды:'
                                                                                           '\n1. Сообщить ССО, если утечка охлаждающей воды находиться внутри оборудования и закрыть запорную арматуру'
                                                                                           '\n2. Cообщить ССО и инженерную службу, если утечка охлаждающей воды находиться в магистрали до технологического оборудования ')


        elif message.text == 'Нет_5':
            with open("Проверка инженерии на PVD " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка охлаждающей воды в зоне PVD ОТСУТСВУЕТ ")
                )
            file.close()
            bot.reply_to(message, ' Информация зафиксировано в  '+ hour+':'+ minute +  ' по отсутствию утечек охлаждающей воды на оборудованиях PVD ')





        elif message.text == 'Есть звук травления на PVD':
            with open("Проверка инженерии на PVD " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне PVD обнаружено звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PVD есть звук травления воздуха. \n1. Сообщить ССО, '

                                                                                           'если травление воздуха происходит внутри оборудования. \n2. Сообщить дежурному от инженерной службы и сообщить ССО, если травление воздуха происходит в магистральной линии (до оборудования).   ')



        elif message.text == "Нет звука травления на PVD":
            with open("Проверка инженерии на PVD " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне PVD отсутствует звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время '+ hour+':'+ minute +  ' в зоне PVD отсутствует травление воздуха')





        elif message.text == 'Кабель/эле-ика нарушена на PVD':
            with open("Проверка инженерии на PVD " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне PVD обнаружено повреждение электроники и/или кабеля  ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PVD обнаружено повреждение электроники и/или кабеля. \n1. Сообщить ССО, '

                                                                                           'если повреждение внутри оборудования. \n2. Сообщить дежурному электрику от инженерной службы и сообщить ССО, если повреждение находиться вне оборудования (до оборудования).   ')



        elif message.text == "Кабель/эле-ика НЕ нарушена на PVD":

            with open("Проверка инженерии на PVD " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне PVD отсутствует повреждение электроники и/или кабеля ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PVD отсутствует повреждение электроники и/или кабеля')








        elif message.text == 'Да чисто в зоне Металлизации':

            with open("Проверка чистоты в зоне оборудований " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Металлизации чисто ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время '+ hour+':'+ minute +  ' в зоне Металлизации чисто')



        elif message.text == 'Нет не чисто в зоне Металлизации':

            with open("Проверка чистоты в зоне оборудований " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Металлизации НЕ чисто ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время '+ hour+':'+ minute +  ' в зоне Металлизации НЕ чисто. Требуеться'
                                                                                        ' организовать уборку мусора. ')


        elif message.text == 'Есть течь охлаждающей воды на Металлизации':
            with open("Проверка инженерии на Металлизации " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка охлаждающей воды в зоне Металлизации обнаружено ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Металлизации обнаружено утечки охлаждающей воды:'
                                                                                           '\n1. Сообщить ССО, если утечка охлаждающей воды находиться внутри оборудования и закрыть запорную арматуру'
                                                                                           '\n2. Cообщить ССО и инженерную службу, если утечка охлаждающей воды находиться в магистрали до технологического оборудования ')


        elif message.text == 'Нет течи охлаждающей воды на Металлизации':
            with open("Проверка инженерии на Металлизации " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка охлаждающей воды в зоне Металлизации ОТСУТСВУЕТ ")
                )
            file.close()
            bot.reply_to(message, ' Информация зафиксировано в  '+ hour+':'+ minute +  ' по отсутствию утечек охлаждающей воды на оборудованиях Металлизации ')



        elif message.text == 'Есть звук травления на Металлизации':
            with open("Проверка инженерии на Металлизации " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Металлизации обнаружено звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Металлизации есть звук травления воздуха. \n1. Сообщить ССО, '

                                                                                           'если травление воздуха происходит внутри оборудования. \n2. Сообщить дежурному от инженерной службы и сообщить ССО, если травление воздуха происходит в магистральной линии (до оборудования).   ')


        elif message.text == "Нет звука травления на Металлизации":
            with open("Проверка инженерии на Металлизации " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Металлизации отсутствует звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время '+ hour+':'+ minute +  ' в зоне Металлизации отсутствует травление воздуха')



        elif message.text == 'Кабель/эле-ика нарушена на Металлизации':
            with open("Проверка инженерии на Металлизации " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Металлизации обнаружено повреждение электроники и/или кабеля  ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Металлизации обнаружено повреждение электроники и/или кабеля. \n1. Сообщить ССО, '

                                                                                           'если повреждение внутри оборудования. \n2. Сообщить дежурному электрику от инженерной службы и сообщить ССО, если повреждение находиться вне оборудования (до оборудования).   ')



        elif message.text == "Кабель/эле-ика НЕ нарушена на Металлизации":

            with open("Проверка инженерии на Металлизации " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Металлизации отсутствует повреждение электроники и/или кабеля ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Металлизации отсутствует повреждение электроники и/или кабеля')




        elif message.text == 'Есть звук травления на Фотоотджиге':
            with open("Проверка инженерии на Фотоотджиге " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Фотоотджига обнаружено звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Фотоотджига есть звук травления воздуха. \n1. Сообщить ССО, '

                                                                                           'если травление воздуха происходит внутри оборудования. \n2. Сообщить дежурному от инженерной службы и сообщить ССО, если травление воздуха происходит в магистральной линии (до оборудования).   ')


        elif message.text == "Нет звука травления на Фотоотджиге":
            with open("Проверка инженерии на Фотоотджиге " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Фотоотджига отсутствует звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время '+ hour+':'+ minute +  ' в зоне Фотоотджига отсутствует травление воздуха')



        elif message.text == 'Да чисто в зоне фотоотджига':

            with open("Проверка чистоты в зоне оборудований " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Фотоотджига чисто ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время '+ hour+':'+ minute +  ' в зоне Фотоотджига чисто')


        elif message.text == 'Нет не чисто в зоне Фотоотджига':

            with open("Проверка чистоты в зоне оборудований " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Фотоотджига НЕ чисто ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время '+ hour+':'+ minute +  ' в зоне Фотоотджига НЕ чисто. Требуеться'
                                                                                        ' организовать уборку мусора. ')


        elif message.text == 'Кабель/эле-ика нарушена на Фотоотджиге':
            with open("Проверка инженерии на Фотоотджиге " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Фотоотджига обнаружено повреждение электроники и/или кабеля  ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Фотоотджига обнаружено повреждение электроники и/или кабеля. \n1. Сообщить ССО, '

                                                                                           'если повреждение внутри оборудования. \n2. Сообщить дежурному электрику от инженерной службы и сообщить ССО, если повреждение находиться вне оборудования (до оборудования).   ')



        elif message.text == "Кабель/эле-ика НЕ нарушена на Фотоотджиге":

            with open("Проверка инженерии на Фотоотджиге " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Фотоотджига отсутствует повреждение электроники и/или кабеля ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Фотоотджига отсутствует повреждение электроники и/или кабеля')




        elif message.text == 'YES_1':
            with open("Проверка инженерии на Фотоотджиге " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка охлаждающей воды в зоне Фотоотджига обнаружено ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Фотоотджига обнаружено утечки охлаждающей воды:'
                                                                                           '\n1. Сообщить ССО, если утечка охлаждающей воды находиться внутри оборудования и закрыть запорную арматуру'
                                                                                           '\n2. Cообщить ССО и инженерную службу, если утечка охлаждающей воды находиться в магистрали до технологического оборудования ')



        elif message.text == 'NO_1':
            with open("Проверка инженерии на Фотоотджиге " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка охлаждающей воды в зоне Фотоотджига ОТСУТСВУЕТ ")
                )
            file.close()
            bot.reply_to(message,
                         ' Информация зафиксировано в  ' + hour + ':' + minute + ' по отсутствию утечек охлаждающей воды на оборудованиях Фотоотджига ')






        elif message.text == 'Есть звук травления воздуха в зоне CIS':
            with open("Проверка инженерии на CIS " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне CIS обнаружено звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне CIS есть звук травления воздуха. \n1. Сообщить ССО, '

                                                                                           'если травление воздуха происходит внутри оборудования. \n2. Сообщить дежурному от инженерной службы и сообщить ССО, если травление воздуха происходит в магистральной линии (до оборудования).   ')


        elif message.text == "Нет звука травления воздуха в зоне CIS":
            with open("Проверка инженерии на CIS " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне CIS отсутствует звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время '+ hour+':'+ minute +  ' в зоне CIS отсутствует травление воздуха')





        elif message.text == 'Да чисто в зоне CIS':

            with open("Проверка чистоты в зоне оборудований " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне CIS чисто ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время '+ hour+':'+ minute +  ' в зоне CIS чисто')



        elif message.text == 'Нет не чисто в зоне CIS':

            with open("Проверка чистоты в зоне оборудований " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне CIS НЕ чисто ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время '+ hour+':'+ minute +  ' в зоне CIS НЕ чисто. Требуеться'
                                                                                        ' организовать уборку мусора. ')


        elif message.text == 'Кабель нарушен в зоне CIS':
            with open("Проверка инженерии на CIS " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне CIS обнаружено повреждение электроники и/или кабеля  ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне CIS обнаружено повреждение электроники и/или кабеля. \n1. Сообщить ССО, '

                                                                                           'если повреждение внутри оборудования. \n2. Сообщить дежурному электрику от инженерной службы и сообщить ССО, если повреждение находиться вне оборудования (до оборудования).   ')



        elif message.text == "Кабель НЕ нарушен в зоне CIS":

            with open("Проверка инженерии на CIS " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне CIS отсутствует повреждение электроники и/или кабеля ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне CIS отсутствует повреждение электроники и/или кабеля')


















# Ночная смена________________________

    elif result.tm_hour > 20:

        # 10.2 фиксирование результатов пломбы на ящике, когда она целая
        if message.text == 'Да 3':

            with open("Паста за ночную смену " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Пломба на ящике с пастой целая, которая принята ПС ФЭП")
                )
            file.close()
            bot.reply_to(message,
                     ' Зафиксировано в ' + hour + ':' + minute + ', что пломба на ящике (на балансе ПС ФЭП) целая')

        # 10.3 фиксирование результатов пломбы на ящике, когда она НЕ целая
        elif message.text == 'Нет 3':

            with open("Паста за ночную смену " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Пломба на ящике с пастой НЕ целая, которая принята ПС ФЭП")
                )
            file.close()
            bot.reply_to(message,
                         ' Зафиксировано в  ' + hour + ':' + minute + ', что пломба на ящике НЕ целая, которая принята ПС ФЭП')



        # 10.4 результаты проверки холодильника №1, когда она не работает
        elif message.text == 'Не работает 1':

            with open("Паста за ночную смену " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Обнаружено, что холодильник №1 НЕ работает")
                )
            file.close()
            bot.reply_to(message,
                        'Информация зафиксировано в  ' + hour + ':' + minute + ', что холодильник №1 не работает. \nНеобходимо сделать следующее согласно Операционной Карте:\n'
                                                                            '\n1. Если также 2-ой холодильник не работает, необходимо вызвать электриков и подключить дизель генератор.\n'
                                                                            '\n2. Если только 1-ый холодильник не работает, необходимо пасту переставить с 1-ого холодильника на 2-ой холодильник.\n'
                                                                            '\n3. Если только 1-ый холодильник не работает и паста не влезает в 2-ой холодильник, то необходимо перенести '
                                                                            'пасту в 3-ий холодильник, для включения 3-го холодильника необходимо вызвать электрика ')

        # 10.5 результаты проверки холодильника №1, когда она находиться в требуемом диапазоне температуры
        elif message.text == 'Да_1':
            with open("Паста за ночную смену " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В холодильнике №1 температура находиться в диапазоне от -18 гр до -21 гр")
                )
            file.close()
            bot.reply_to(message,
                        'Информация зафиксировано в  ' + hour + ':' + minute + ', что в холодильнике температура находиться в диапазоне от -18 гр до -21 гр')

        # 10.6 результаты проверки холодильника №1, когда она находиться НЕ требуемом диапазоне температуры
        elif message.text == 'Нет_1':
            with open("Паста за ночную смену " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), "В холодильнике №1 температура НЕ находиться в диапазоне от -18 гр до -21 гр")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано в  ' + hour + ':' + minute + ', что в холодильнике температура не находиться в диапазоне от -18 гр до -21 гр\n'
                                                                            '\nНеобходимо сделать следующее согласно Операционной Карте:\n'
                                                                            '\n1. Если температура выше -16 гр но ниже -15 гр то сделать следующее:\n'
                                                                            '\n 1.1 Мониторить температуру в течении 10 минут, если температура не отпускаеться, то необходимо перенести пасту с'
                                                                            '       с холодильника №1 в холодильник №2 (это только в том случае если у холодильника №2 температуара'
                                                                            '       находиться в диапазоне от -18 гр до -21 гр)\n '
                                                                            '\n2. Если температура выше -15 градусов, то перенести пасту с холодильника №1 в холодильник №2\n'
                                                                            '\n3. Если температура выше -15 градусов и если нет мест в холодильнике №2 то пасту перенести 3-ий холодильник')

        # 10.7 результаты проверки холодильника №1, когда она НЕ работает
        elif message.text == 'Не работает 2':
            with open("Паста за ночную смену " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Обнаружено, что холодильник №2 НЕ работает")
                )
            file.close()
            bot.reply_to(message,
                        'Информация зафиксировано  ' + hour + ':' + minute + ', что холодильник №2 не работает. \nНеобходимо сделать следующее согласно Операционной Карте:\n'
                                                                          '\n1. Если также 1-ый холодильник не работает, необходимо вызвать электриков и подключить дизель генератор.\n'
                                                                          '\n2. Если только 1-ый холодильник не работает, необходимо пасту переставить с 1-ого холодильника на 2-ой холодильник.\n'
                                                                          '\n3. Если только 1-ый холодильник не работает и паста не влезает в 2-ой холодильник, то необходимо перенести '
                                                                          'пасту в 3-ий холодильник, для включения 3-го холодильника необходимо вызвать электрика ')

        # 10.8 результаты проверки холодильника №1, когда температура находиться в требуемом дипазоне
        elif message.text == 'Да_2':
            with open("Паста за ночную смену " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В холодильнике №2 температура находиться в диапазоне от -18 гр до -21 гр")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано в  ' + hour + ':' + minute + ', что в холодильнике №2 температура находиться в диапазоне от -18 гр до -21 гр')

            # 10.9 результаты проверки холодильника №1, когда температура находиться в НЕ требуемом дипазоне
        elif message.text == 'Нет_2':
            with open("Паста за ночную смену " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), "В холодильнике №2 температура НЕ находиться в диапазоне от -18 гр до -21 гр")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано в  ' + hour + ':' + minute + ', что в холодильнике №2 температура не находиться в диапазоне от -18 гр до -21 гр\n'
                                                                                '\nНеобходимо сделать следующее согласно Операционной Карте:\n'
                                                                                '\n1. Если температура выше -16 гр но ниже -15 гр то сделать следующее:\n'
                                                                                '\n 1.1 Мониторить температуру в течении 10 минут, если температура не отпускаеться, то необходимо перенести пасту с'
                                                                                '       с холодильника №2 в холодильник №1 (это только в том случае если у холодильника №1 температуара'
                                                                                '       находиться в диапазоне от -18 гр до -21 гр)\n '
                                                                                '\n2. Если температура выше -15 градусов, то перенести пасту с холодильника №2 в холодильник №1\n'
                                                                                '\n3. Если температура выше -15 градусов и если нет мест в холодильнике №1 то пасту перенести 3-ий холодильник')







        elif message.text == 'Нет 3':
            with open("Паста за ночную смену " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Зафиксировано, что пломба на ящике не целая")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано в  '+ hour+':'+ minute +  ', что Пломба не цела. Необходимо:'
                                                                             '\n1. Фотографировать сорванную пломбу.'
                                                                             '\n2. Фотографировать содержимое ящика.'
                                                                             '\n3. Произвести подсчет количества банок внутри ящика'
                                                                             '\n4. Сообщить начальника ПС ФЭП')


        elif message.text == 'Да 3':
            with open("Паста за ночную смену " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Зафиксировано, что пломба на ящике целая")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано в  '+ hour+':'+ minute +  ', что пломба целая на ящике')



        elif message.text == 'В зоне WIS ЕСТЬ звук травления воздуха':
            with open("Ночная проверка инженерии на WIS " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне WIS обнаружено звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне WIS есть звук травления воздуха. \n1. Сообщить ССО, '

                                                                                           'если травление воздуха происходит внутри оборудования. \n2. Сообщить дежурному от инженерной службы и сообщить ССО, если травление воздуха происходит в магистральной линии (до оборудования).   ')



        elif message.text == "В зоне WIS НЕТ звук травления воздуха":

            with open("Ночная проверка инженерии на WIS " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне WIS отсутствует звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне WIS отсутствует травление воздуха')



        elif message.text == 'Кабель/эле-ика нарушена на WIS':
            with open("Ночная проверка инженерии на WIS " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне WIS обнаружено повреждение электроники и/или кабеля  ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне WIS обнаружено повреждение электроники и/или кабеля. \n1. Сообщить ССО, '

                                                                                           'если повреждение внутри оборудования. \n2. Сообщить дежурному электрику от инженерной службы и сообщить ССО, если повреждение находиться вне оборудования (до оборудования).   ')


        elif message.text == "Кабель/эле-ика НЕ нарушена на WIS":

            with open("Ночная проверка инженерии на WIS " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне WIS отсутствует повреждение электроники и/или кабеля ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне WIS отсутствует повреждение электроники и/или кабеля')









        elif message.text == 'Есть звук травления воздуха зоне Текст-ия':
            with open("Ночная проверка инженерии на Текстурировании " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Текстурирования обнаружено звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Текстурирования есть звук травления воздуха. \n1. Сообщить ССО, '

                                                                                           'если травление воздуха происходит внутри оборудования. \n2. Сообщить дежурному от инженерной службы и сообщить ССО, если травление воздуха происходит в магистральной линии (до оборудования).   ')



        elif message.text == "Нет звука травления воздуха зоне Текст-ия":
            with open("Ночная проверка инженерии на Текстурировании " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Текстурирования отсутствует звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Текстурирования отсутствует травление воздуха')



        elif message.text == 'Кабель/эле-ика нарушена на текстурировании':
            with open("Ночная проверка инженерии на Текстурировании " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Текстурировании обнаружено повреждение электроники и/или кабеля  ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Текстурирования обнаружено повреждение электроники и/или кабеля. \n1. Сообщить ССО, '

                                                                                           'если повреждение внутри оборудования. \n2. Сообщить дежурному электрику от инженерной службы и сообщить ССО, если повреждение находиться вне оборудования (до оборудования).   ')


        elif message.text == "Кабель/эле-ика НЕ нарушена на текстурировании":

            with open("Ночная проверка инженерии на Текстурировании " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Текстурирования отсутствует повреждение электроники и/или кабеля ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Текстурирования отсутствует повреждение электроники и/или кабеля')

            # 10.12 результаты проверки Текстурированя, когда течь воды обнаружено



        elif message.text == 'YES_2':
            with open("Ночная проверка инженерии " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка DI воды в зоне Текстурирования обнаружено ")
                )
            file.close()

            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Текстурирования обнаружено утечки DI воды:'
                                                                                           '\n1. Сообщить ССО если утечка DI воды находиться внутри оборудования и закрыть запорную арматуру'
                                                                                           '\n2. Cообщить ССО и инженерную службу если утчека DI воды находиться в магистрали до технологического оборудования ')


        # 10.13 результаты проверки Текстурированя, когда течь воды отсутсвует
        elif message.text == 'NO_2':
            with open("Ночная проверка инженерии на Текстурировании " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка DI воды в зоне Текстурирования отсутствует")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано в  ' + hour + ':' + minute + ' по отсутствию утечек DI воды в зоне Текстурирования ')





        elif message.text == 'Есть течь охлаждающей воды на Текстурировании':
            with open("Ночная проверка инженерии на Текстурировании " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка охлаждающей воды в зоне Текстурирования обнаружено ")
                )
            file.close()

            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Текстурирования обнаружено утечки охлаждающей воды:'
                                                                                           '\n1. Сообщить ССО, если утечка охлаждающей воды находиться внутри оборудования и закрыть запорную арматуру'
                                                                                           '\n2. Cообщить ССО и инженерную службу, если утчека охлаждающей воды находиться в магистрали до технологического оборудования ')


        # 10.13 результаты проверки Текстурированя, когда течь воды отсутсвует
        elif message.text == 'Нет течи охлаждающей воды на Текстурировании':
            with open("Ночная проверка инженерии на Текстурировании " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка охлаждающей воды в зоне Текстурирования отсутствует")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано в  ' + hour + ':' + minute + ' по отсутствию утечек охлаждающей воды в зоне Текстурирования ')






        elif message.text == 'Да_4':
            with open("Ночная проверка инженерии на PECVD " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка охлаждающей воды в зоне PECVD обнаружено ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PECVD обнаружено утечки охлаждающей воды:'
                                                                                           '\n1. Сообщить ССО, если утечка охлаждающей воды находиться внутри оборудования и закрыть запорную арматуру'
                                                                                           '\n2. Cообщить ССО и инженерную службу, если утчека охлаждающей воды находиться в магистрали до технологического оборудования ')



        elif message.text == 'Нет_4':
            with open("Ночная проверка инженерии на PECVD " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка охлаждающей воды в зоне PECVD ОТСУТСВУЕТ ")
                )
            file.close()
            bot.reply_to(message,
                         ' Информация зафиксировано в  ' + hour + ':' + minute + ' по отсутствию утечек охлаждающей воды на оборудованиях PECVD ')




        elif message.text == 'Есть утечки стоков на PECVD':
            with open("Ночная проверка инженерии на PECVD " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечки стоков на PECVD обнаружено ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PECVD обнаружено утечки стоков:'
                                                                                           '\n Cообщить ССО и инженерную службу, касаемо наличии утечки стоков')



        elif message.text == 'Отсутствует утечки стоков на PECVD':
            with open("Ночная проверка инженерии на PECVD " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка стоков в зоне PECVD ОТСУТСВУЕТ ")
                )
            file.close()
            bot.reply_to(message,
                         ' Информация зафиксировано в  ' + hour + ':' + minute + ' по отсутствию утечек стоков в зоне PECVD ')




        elif message.text == 'Кабель/эле-ика нарушена на PECVD':
            with open("Ночная проверка инженерии на PECVD " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне PECVD обнаружено повреждение электроники и/или кабеля  ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PECVD обнаружено повреждение электроники и/или кабеля. \n1. Сообщить ССО, '

                                                                                           'если повреждение внутри оборудования. \n2. Сообщить дежурному электрику от инженерной службы и сообщить ССО, если повреждение находиться вне оборудования (до оборудования).   ')



        elif message.text == "Кабель/эле-ика НЕ нарушена на PECVD":

            with open("Ночная проверка инженерии на PECVD " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне PECVD отсутствует повреждение электроники и/или кабеля ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PECVD отсутствует повреждение электроники и/или кабеля')



        elif message.text == 'Есть звук травления в зоне PECVD':
            with open("Ночная проверка инженерии на PECVD " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне PECVD обнаружено звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PECVD есть звук травления воздуха. \n1. Сообщить ССО, '

                                                                                           'если травление воздуха происходит внутри оборудования. \n2. Сообщить дежурному от инженерной службы и сообщить ССО, если травление воздуха происходит в магистральной линии (до оборудования).   ')



        elif message.text == "Нет звука травления в зоне PECVD":
            with open("Ночная проверка инженерии на PECVD " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне PECVD отсутствует звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PECVD отсутствует травление воздуха')







        elif message.text == 'Да_5':
            with open("Ночная проверка инженерии на PVD " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка охлаждающей воды в зоне PVD обнаружено ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PVD обнаружено утечки охлаждающей воды:'
                                                                                           '\n1. Сообщить ССО, если утечка охлаждающей воды находиться внутри оборудования и закрыть запорную арматуру'
                                                                                           '\n2. Cообщить ССО и инженерную службу, если утечка охлаждающей воды находиться в магистрали до технологического оборудования ')


        elif message.text == 'Нет_5':
            with open("Ночная проверка инженерии на PVD " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка охлаждающей воды в зоне PVD ОТСУТСВУЕТ ")
                )
            file.close()
            bot.reply_to(message,
                         ' Информация зафиксировано в  ' + hour + ':' + minute + ' по отсутствию утечек охлаждающей воды на оборудованиях PVD ')





        elif message.text == 'Есть звук травления на PVD':
            with open("Ночная проверка инженерии на PVD " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне PVD обнаружено звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PVD есть звук травления воздуха. \n1. Сообщить ССО, '

                                                                                           'если травление воздуха происходит внутри оборудования. \n2. Сообщить дежурному от инженерной службы и сообщить ССО, если травление воздуха происходит в магистральной линии (до оборудования).   ')



        elif message.text == "Нет звука травления на PVD":
            with open("Ночная проверка инженерии на PVD " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне PVD отсутствует звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PVD отсутствует травление воздуха')





        elif message.text == 'Кабель/эле-ика нарушена на PVD':
            with open("Ночная проверка инженерии на PVD " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне PVD обнаружено повреждение электроники и/или кабеля  ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PVD обнаружено повреждение электроники и/или кабеля. \n1. Сообщить ССО, '

                                                                                           'если повреждение внутри оборудования. \n2. Сообщить дежурному электрику от инженерной службы и сообщить ССО, если повреждение находиться вне оборудования (до оборудования).   ')



        elif message.text == "Кабель/эле-ика НЕ нарушена на PVD":

            with open("Ночная проверка инженерии на PVD " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне PVD отсутствует повреждение электроники и/или кабеля ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PVD отсутствует повреждение электроники и/или кабеля')







        elif message.text == 'Есть течь охлаждающей воды на Металлизации':
            with open("Ночная проверка инженерии на Металлизации " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка охлаждающей воды в зоне Металлизации обнаружено ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Металлизации обнаружено утечки охлаждающей воды:'
                                                                                           '\n1. Сообщить ССО, если утечка охлаждающей воды находиться внутри оборудования и закрыть запорную арматуру'
                                                                                           '\n2. Cообщить ССО и инженерную службу, если утечка охлаждающей воды находиться в магистрали до технологического оборудования ')


        elif message.text == 'Нет течи охлаждающей воды на Металлизации':
            with open("Ночная проверка инженерии на Металлизации " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка охлаждающей воды в зоне Металлизации ОТСУТСВУЕТ ")
                )
            file.close()
            bot.reply_to(message,
                         ' Информация зафиксировано в  ' + hour + ':' + minute + ' по отсутствию утечек охлаждающей воды на оборудованиях Металлизации ')



        elif message.text == 'Есть звук травления на Металлизации':
            with open("Ночная проверка инженерии на Металлизации " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Металлизации обнаружено звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Металлизации есть звук травления воздуха. \n1. Сообщить ССО, '

                                                                                           'если травление воздуха происходит внутри оборудования. \n2. Сообщить дежурному от инженерной службы и сообщить ССО, если травление воздуха происходит в магистральной линии (до оборудования).   ')


        elif message.text == "Нет звука травления на Металлизации":
            with open("Ночная проверка инженерии на Металлизации " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Металлизации отсутствует звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Металлизации отсутствует травление воздуха')



        elif message.text == 'Кабель/эле-ика нарушена на Металлизации':
            with open("Ночная проверка инженерии на Металлизации " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Металлизации обнаружено повреждение электроники и/или кабеля  ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Металлизации обнаружено повреждение электроники и/или кабеля. \n1. Сообщить ССО, '

                                                                                           'если повреждение внутри оборудования. \n2. Сообщить дежурному электрику от инженерной службы и сообщить ССО, если повреждение находиться вне оборудования (до оборудования).   ')



        elif message.text == "Кабель/эле-ика НЕ нарушена на Металлизации":

            with open("Ночная проверка инженерии на Металлизации " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Металлизации отсутствует повреждение электроники и/или кабеля ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Металлизации отсутствует повреждение электроники и/или кабеля')




        elif message.text == 'Есть звук травления на Фотоотджиге':
            with open("Ночная проверка инженерии на Фотооджиге " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Фотоотджига обнаружено звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Фотоотджига есть звук травления воздуха. \n1. Сообщить ССО, '

                                                                                           'если травление воздуха происходит внутри оборудования. \n2. Сообщить дежурному от инженерной службы и сообщить ССО, если травление воздуха происходит в магистральной линии (до оборудования).   ')


        elif message.text == "Нет звука травления на Фотоотджиге":
            with open("Ночная проверка инженерии на Фотооджиге " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Фотоотджига отсутствует звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Фотоотджига отсутствует травление воздуха')




        elif message.text == 'Кабель/эле-ика нарушена на Фотоотджиге':
            with open("Ночная проверка инженерии на Фотооджиге " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Фотоотджига обнаружено повреждение электроники и/или кабеля  ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Фотоотджига обнаружено повреждение электроники и/или кабеля. \n1. Сообщить ССО, '

                                                                                           'если повреждение внутри оборудования. \n2. Сообщить дежурному электрику от инженерной службы и сообщить ССО, если повреждение находиться вне оборудования (до оборудования).   ')



        elif message.text == "Кабель/эле-ика НЕ нарушена на Фотоотджиге":

            with open("Ночная проверка инженерии на Фотооджиге "
                      " " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Фотоотджига отсутствует повреждение электроники и/или кабеля ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Фотоотджига отсутствует повреждение электроники и/или кабеля')





        elif message.text == 'Есть звук травления воздуха в зоне CIS':
            with open("Ночная проверка инженерии на CIS " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне CIS обнаружено звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне CIS есть звук травления воздуха. \n1. Сообщить ССО, '

                                                                                           'если травление воздуха происходит внутри оборудования. \n2. Сообщить дежурному от инженерной службы и сообщить ССО, если травление воздуха происходит в магистральной линии (до оборудования).   ')


        elif message.text == "Нет звука травления воздуха в зоне CIS":
            with open("Ночная проверка инженерии на CIS " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне CIS отсутствует звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне CIS отсутствует травление воздуха')




        elif message.text == 'Кабель нарушен в зоне CIS':
            with open("Ночная проверка инженерии на CIS " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне CIS обнаружено повреждение электроники и/или кабеля  ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне CIS обнаружено повреждение электроники и/или кабеля. \n1. Сообщить ССО, '

                                                                                           'если повреждение внутри оборудования. \n2. Сообщить дежурному электрику от инженерной службы и сообщить ССО, если повреждение находиться вне оборудования (до оборудования).   ')



        elif message.text == "Кабель НЕ нарушен в зоне CIS":

            with open("Ночная проверка инженерии на CIS " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне CIS отсутствует повреждение электроники и/или кабеля ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне CIS отсутствует повреждение электроники и/или кабеля')




    # Фиксация результатов после 00:00

    elif result.tm_hour <8:
        if message.text == "Отчет ночной смены":


            w = open("Ночная проверка инженерии на WIS " + day + "." + month + "." + year + ".csv", "rb")
            requests.get(f'{URL}{Token}/sendDocument', data={'chat_id': test_group_chat}, files={'document': w})

            f = open("Паста за ночную смену " + day + "." + month + "." + year + ".csv", "rb")
            requests.get(f'{URL}{Token}/sendDocument', data={'chat_id': test_group_chat}, files={'document': f})

            m = open("Ночная проверка инженерии на Текстурировании " + day + "." + month + "." + year + ".csv", "rb")
            requests.get(f'{URL}{Token}/sendDocument', data={'chat_id': test_group_chat}, files={'document': m})

            z = open("Ночная проверка инженерии на PECVD " + day + "." + month + "." + year + ".csv", "rb")
            requests.get(f'{URL}{Token}/sendDocument', data={'chat_id': test_group_chat}, files={'document': z})

            v = open("Ночная проверка инженерии на PVD " + day + "." + month + "." + year + ".csv", "rb")
            requests.get(f'{URL}{Token}/sendDocument', data={'chat_id': test_group_chat}, files={'document': v})

            n = open("Ночная проверка инженерии на Металлизации " + day + "." + month + "." + year + ".csv", "rb")
            requests.get(f'{URL}{Token}/sendDocument', data={'chat_id': test_group_chat}, files={'document': n})

            l = open("Ночная проверка инженерии на Фотооджиге " + day + "." + month + "." + year + ".csv", "rb")
            requests.get(f'{URL}{Token}/sendDocument', data={'chat_id': test_group_chat}, files={'document': l})

            d = open("Ночная проверка инженерии на CIS " + day + "." + month + "." + year + ".csv", "rb")
            requests.get(f'{URL}{Token}/sendDocument', data={'chat_id': test_group_chat}, files={'document': d})

            с = open("Проверка чистоты в зоне оборудований " + day + "." + month + "." + year + ".csv", "rb")
            requests.get(f'{URL}{Token}/sendDocument', data={'chat_id': test_group_chat}, files={'document': с})

            bot.send_message(message.chat.id, 'Отчет отправлен')



        elif message.text == 'Да 3':

            with open("Паста за ночную смену " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Пломба на ящике с пастой целая, которая принята ПС ФЭП")
                )
            file.close()
            bot.reply_to(message,
                     ' Зафиксировано в  ' + hour + ':' + minute + ', что пломба на ящике (на балансе ПС ФЭП) целая')

        # 10.3 фиксирование результатов пломбы на ящике, когда она НЕ целая
        elif message.text == 'Нет 3':

            with open("Паста за ночную смену " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Пломба на ящике с пастой НЕ целая, которая принята ПС ФЭП")
                )
            file.close()
            bot.reply_to(message,
                         ' Зафиксировано в  ' + hour + ':' + minute + ', что пломба на ящике НЕ целая, которая принята ПС ФЭП')

        # 10.4 результаты проверки холодильника №1, когда она не работает
        elif message.text == 'Не работает 1':

            with open("Паста за ночную смену " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Обнаружено, что холодильник №1 НЕ работает")
                )
            file.close()
            bot.reply_to(message,
                        'Информация зафиксировано в  ' + hour + ':' + minute + ', что холодильник №1 не работает. \nНеобходимо сделать следующее согласно Операционной Карте:\n'
                                                                            '\n1. Если также 2-ой холодильник не работает, необходимо вызвать электриков и подключить дизель генератор.\n'
                                                                            '\n2. Если только 1-ый холодильник не работает, необходимо пасту переставить с 1-ого холодильника на 2-ой холодильник.\n'
                                                                            '\n3. Если только 1-ый холодильник не работает и паста не влезает в 2-ой холодильник, то необходимо перенести '
                                                                            'пасту в 3-ий холодильник, для включения 3-го холодильника необходимо вызвать электрика ')

        # 10.5 результаты проверки холодильника №1, когда она находиться в требуемом диапазоне температуры
        elif message.text == 'Да_1':
            with open("Паста за ночную смену " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В холодильнике №1 температура находиться в диапазоне от -18 гр до -21 гр")
                )
            file.close()
            bot.reply_to(message,
                        'Информация зафиксировано в  ' + hour + ':' + minute + ', что в холодильнике температура находиться в диапазоне от -18 гр до -21 гр')

        # 10.6 результаты проверки холодильника №1, когда она находиться НЕ требуемом диапазоне температуры
        elif message.text == 'Нет_1':
            with open("Паста за ночную смену " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), "В холодильнике №1 температура НЕ находиться в диапазоне от -18 гр до -21 гр")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано в  ' + hour + ':' + minute + ', что в холодильнике температура не находиться в диапазоне от -18 гр до -21 гр\n'
                                                                            '\nНеобходимо сделать следующее согласно Операционной Карте:\n'
                                                                            '\n1. Если температура выше -16 гр но ниже -15 гр то сделать следующее:\n'
                                                                            '\n 1.1 Мониторить температуру в течении 10 минут, если температура не отпускаеться, то необходимо перенести пасту с'
                                                                            '       с холодильника №1 в холодильник №2 (это только в том случае если у холодильника №2 температуара'
                                                                            '       находиться в диапазоне от -18 гр до -21 гр)\n '
                                                                            '\n2. Если температура выше -15 градусов, то перенести пасту с холодильника №1 в холодильник №2\n'
                                                                            '\n3. Если температура выше -15 градусов и если нет мест в холодильнике №2 то пасту перенести 3-ий холодильник')

        # 10.7 результаты проверки холодильника №1, когда она НЕ работает
        elif message.text == 'Не работает 2':
            with open("Паста за ночную смену " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Обнаружено, что холодильник №2 НЕ работает")
                )
            file.close()
            bot.reply_to(message,
                        'Информация зафиксировано  ' + hour + ':' + minute + ', что холодильник №2 не работает. \nНеобходимо сделать следующее согласно Операционной Карте:\n'
                                                                          '\n1. Если также 1-ый холодильник не работает, необходимо вызвать электриков и подключить дизель генератор.\n'
                                                                          '\n2. Если только 1-ый холодильник не работает, необходимо пасту переставить с 1-ого холодильника на 2-ой холодильник.\n'
                                                                          '\n3. Если только 1-ый холодильник не работает и паста не влезает в 2-ой холодильник, то необходимо перенести '
                                                                          'пасту в 3-ий холодильник, для включения 3-го холодильника необходимо вызвать электрика ')

        # 10.8 результаты проверки холодильника №1, когда температура находиться в требуемом дипазоне
        elif message.text == 'Да_2':
            with open("Паста за ночную смену " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В холодильнике №2 температура находиться в диапазоне от -18 гр до -21 гр")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано в  ' + hour + ':' + minute + ', что в холодильнике №2 температура находиться в диапазоне от -18 гр до -21 гр')

            # 10.9 результаты проверки холодильника №1, когда температура находиться в НЕ требуемом дипазоне
        elif message.text == 'Нет_2':
            with open("Паста за ночную смену " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), "В холодильнике №2 температура НЕ находиться в диапазоне от -18 гр до -21 гр")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано в  ' + hour + ':' + minute + ', что в холодильнике №2 температура не находиться в диапазоне от -18 гр до -21 гр\n'
                                                                                '\nНеобходимо сделать следующее согласно Операционной Карте:\n'
                                                                                '\n1. Если температура выше -16 гр но ниже -15 гр то сделать следующее:\n'
                                                                                '\n 1.1 Мониторить температуру в течении 10 минут, если температура не отпускаеться, то необходимо перенести пасту с'
                                                                                '       с холодильника №2 в холодильник №1 (это только в том случае если у холодильника №1 температуара'
                                                                                '       находиться в диапазоне от -18 гр до -21 гр)\n '
                                                                                '\n2. Если температура выше -15 градусов, то перенести пасту с холодильника №2 в холодильник №1\n'
                                                                                '\n3. Если температура выше -15 градусов и если нет мест в холодильнике №1 то пасту перенести 3-ий холодильник')



        elif message.text == 'Нет 3':
            with open("Паста за ночную смену " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Зафиксировано, что пломба на ящике не целая")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано в  '+ hour+':'+ minute +  ', что Пломба не цела. Необходимо:'
                                                                             '\n1. Фотографировать сорванную пломбу.'
                                                                             '\n2. Фотографировать содержимое ящика.'
                                                                             '\n3. Произвести подсчет количества банок внутри ящика'
                                                                             '\n4. Сообщить начальника ПС ФЭП')


        elif message.text == 'Да 3':
            with open("Паста за ночную смену " + day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Зафиксировано, что пломба на ящике целая")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано в  '+ hour+':'+ minute +  ', что пломба целая на ящике')





        elif message.text == 'В зоне WIS ЕСТЬ звук травления воздуха':
            with open("Ночная проверка инженерии на WIS " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне WIS обнаружено звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне WIS есть звук травления воздуха. \n1. Сообщить ССО, '

                                                                                           'если травление воздуха происходит внутри оборудования. \n2. Сообщить дежурному от инженерной службы и сообщить ССО, если травление воздуха происходит в магистральной линии (до оборудования).   ')



        elif message.text == "В зоне WIS НЕТ звук травления воздуха":

            with open("Ночная проверка инженерии на WIS " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне WIS отсутствует звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне WIS отсутствует травление воздуха')



        elif message.text == 'Кабель/эле-ика нарушена на WIS':
            with open("Ночная проверка инженерии на WIS " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне WIS обнаружено повреждение электроники и/или кабеля  ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне WIS обнаружено повреждение электроники и/или кабеля. \n1. Сообщить ССО, '

                                                                                           'если повреждение внутри оборудования. \n2. Сообщить дежурному электрику от инженерной службы и сообщить ССО, если повреждение находиться вне оборудования (до оборудования).   ')


        elif message.text == "Кабель/эле-ика НЕ нарушена на WIS":

            with open("Ночная проверка инженерии на WIS " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне WIS отсутствует повреждение электроники и/или кабеля ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне WIS отсутствует повреждение электроники и/или кабеля')









        elif message.text == 'Есть звук травления воздуха зоне Текст-ия':
            with open("Ночная проверка инженерии на Текстурировании " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Текстурирования обнаружено звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Текстурирования есть звук травления воздуха. \n1. Сообщить ССО, '

                                                                                           'если травление воздуха происходит внутри оборудования. \n2. Сообщить дежурному от инженерной службы и сообщить ССО, если травление воздуха происходит в магистральной линии (до оборудования).   ')



        elif message.text == "Нет звука травления воздуха зоне Текст-ия":
            with open("Ночная проверка инженерии на Текстурировании " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Текстурирования отсутствует звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Текстурирования отсутствует травление воздуха')



        elif message.text == 'Кабель/эле-ика нарушена на текстурировании':
            with open("Ночная проверка инженерии на Текстурировании " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Текстурировании обнаружено повреждение электроники и/или кабеля  ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Текстурирования обнаружено повреждение электроники и/или кабеля. \n1. Сообщить ССО, '

                                                                                           'если повреждение внутри оборудования. \n2. Сообщить дежурному электрику от инженерной службы и сообщить ССО, если повреждение находиться вне оборудования (до оборудования).   ')


        elif message.text == "Кабель/эле-ика НЕ нарушена на текстурировании":

            with open("Ночная проверка инженерии на Текстурировании " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Текстурирования отсутствует повреждение электроники и/или кабеля ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Текстурирования отсутствует повреждение электроники и/или кабеля')

            # 10.12 результаты проверки Текстурированя, когда течь воды обнаружено



        elif message.text == 'YES_2':
            with open("Ночная проверка инженерии на Текстурировании " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка DI воды в зоне Текстурирования обнаружено ")
                )
            file.close()

            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Текстурирования обнаружено утечки DI воды:'
                                                                                           '\n1. Сообщить ССО если утечка DI воды находиться внутри оборудования и закрыть запорную арматуру'
                                                                                           '\n2. Cообщить ССО и инженерную службу если утчека DI воды находиться в магистрали до технологического оборудования ')


        # 10.13 результаты проверки Текстурированя, когда течь воды отсутсвует
        elif message.text == 'NO_2':
            with open("Ночная проверка инженерии на Текстурировании " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка DI воды в зоне Текстурирования отсутствует")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано в  ' + hour + ':' + minute + ' по отсутствию утечек DI воды в зоне Текстурирования ')





        elif message.text == 'Есть течь охлаждающей воды на Текстурировании':
            with open("Ночная проверка инженерии на Текстурировании " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка охлаждающей воды в зоне Текстурирования обнаружено ")
                )
            file.close()

            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Текстурирования обнаружено утечки охлаждающей воды:'
                                                                                           '\n1. Сообщить ССО, если утечка охлаждающей воды находиться внутри оборудования и закрыть запорную арматуру'
                                                                                           '\n2. Cообщить ССО и инженерную службу, если утчека охлаждающей воды находиться в магистрали до технологического оборудования ')


        # 10.13 результаты проверки Текстурированя, когда течь воды отсутсвует
        elif message.text == 'Нет течи охлаждающей воды на Текстурировании':
            with open("Ночная проверка инженерии на Текстурировании " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка охлаждающей воды в зоне Текстурирования отсутствует")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано в  ' + hour + ':' + minute + ' по отсутствию утечек охлаждающей воды в зоне Текстурирования ')






        elif message.text == 'Да_4':
            with open("Ночная проверка инженерии на PECVD " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка охлаждающей воды в зоне PECVD обнаружено ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PECVD обнаружено утечки охлаждающей воды:'
                                                                                           '\n1. Сообщить ССО, если утечка охлаждающей воды находиться внутри оборудования и закрыть запорную арматуру'
                                                                                           '\n2. Cообщить ССО и инженерную службу, если утчека охлаждающей воды находиться в магистрали до технологического оборудования ')



        elif message.text == 'Нет_4':
            with open("Ночная проверка инженерии на PECVD " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка охлаждающей воды в зоне PECVD ОТСУТСВУЕТ ")
                )
            file.close()
            bot.reply_to(message,
                         ' Информация зафиксировано в  ' + hour + ':' + minute + ' по отсутствию утечек охлаждающей воды на оборудованиях PECVD ')




        elif message.text == 'Есть утечки стоков на PECVD':
            with open("Ночная проверка инженерии на PECVD " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечки стоков на PECVD обнаружено ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PECVD обнаружено утечки стоков:'
                                                                                           '\n Cообщить ССО и инженерную службу, касаемо наличии утечки стоков')



        elif message.text == 'Отсутствует утечки стоков на PECVD':
            with open("Ночная проверка инженерии на PECVD " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка стоков в зоне PECVD ОТСУТСВУЕТ ")
                )
            file.close()
            bot.reply_to(message,
                         ' Информация зафиксировано в  ' + hour + ':' + minute + ' по отсутствию утечек стоков в зоне PECVD ')




        elif message.text == 'Кабель/эле-ика нарушена на PECVD':
            with open("Ночная проверка инженерии на PECVD " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне PECVD обнаружено повреждение электроники и/или кабеля  ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PECVD обнаружено повреждение электроники и/или кабеля. \n1. Сообщить ССО, '

                                                                                           'если повреждение внутри оборудования. \n2. Сообщить дежурному электрику от инженерной службы и сообщить ССО, если повреждение находиться вне оборудования (до оборудования).   ')



        elif message.text == "Кабель/эле-ика НЕ нарушена на PECVD":

            with open("Ночная проверка инженерии на PECVD " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне PECVD отсутствует повреждение электроники и/или кабеля ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PECVD отсутствует повреждение электроники и/или кабеля')



        elif message.text == 'Есть звук травления в зоне PECVD':
            with open("Ночная проверка инженерии на PECVD " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне PECVD обнаружено звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PECVD есть звук травления воздуха. \n1. Сообщить ССО, '

                                                                                           'если травление воздуха происходит внутри оборудования. \n2. Сообщить дежурному от инженерной службы и сообщить ССО, если травление воздуха происходит в магистральной линии (до оборудования).   ')



        elif message.text == "Нет звука травления в зоне PECVD":
            with open("Ночная проверка инженерии на PECVD " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне PECVD отсутствует звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PECVD отсутствует травление воздуха')







        elif message.text == 'Да_5':
            with open("Ночная проверка инженерии на PVD " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка охлаждающей воды в зоне PVD обнаружено ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PVD обнаружено утечки охлаждающей воды:'
                                                                                           '\n1. Сообщить ССО, если утечка охлаждающей воды находиться внутри оборудования и закрыть запорную арматуру'
                                                                                           '\n2. Cообщить ССО и инженерную службу, если утечка охлаждающей воды находиться в магистрали до технологического оборудования ')


        elif message.text == 'Нет_5':
            with open("Ночная проверка инженерии на PVD " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка охлаждающей воды в зоне PVD ОТСУТСВУЕТ ")
                )
            file.close()
            bot.reply_to(message,
                         ' Информация зафиксировано в  ' + hour + ':' + minute + ' по отсутствию утечек охлаждающей воды на оборудованиях PVD ')





        elif message.text == 'Есть звук травления на PVD':
            with open("Ночная проверка инженерии на PVD " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне PVD обнаружено звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PVD есть звук травления воздуха. \n1. Сообщить ССО, '

                                                                                           'если травление воздуха происходит внутри оборудования. \n2. Сообщить дежурному от инженерной службы и сообщить ССО, если травление воздуха происходит в магистральной линии (до оборудования).   ')



        elif message.text == "Нет звука травления на PVD":
            with open("Ночная проверка инженерии на PVD " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне PVD отсутствует звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PVD отсутствует травление воздуха')





        elif message.text == 'Кабель/эле-ика нарушена на PVD':
            with open("Ночная проверка инженерии на PVD " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне PVD обнаружено повреждение электроники и/или кабеля  ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PVD обнаружено повреждение электроники и/или кабеля. \n1. Сообщить ССО, '

                                                                                           'если повреждение внутри оборудования. \n2. Сообщить дежурному электрику от инженерной службы и сообщить ССО, если повреждение находиться вне оборудования (до оборудования).   ')



        elif message.text == "Кабель/эле-ика НЕ нарушена на PVD":

            with open("Ночная проверка инженерии на PVD " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне PVD отсутствует повреждение электроники и/или кабеля ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне PVD отсутствует повреждение электроники и/или кабеля')







        elif message.text == 'Есть течь охлаждающей воды на Металлизации':
            with open("Ночная проверка инженерии на Металлизации " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка охлаждающей воды в зоне Металлизации обнаружено ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Металлизации обнаружено утечки охлаждающей воды:'
                                                                                           '\n1. Сообщить ССО, если утечка охлаждающей воды находиться внутри оборудования и закрыть запорную арматуру'
                                                                                           '\n2. Cообщить ССО и инженерную службу, если утечка охлаждающей воды находиться в магистрали до технологического оборудования ')


        elif message.text == 'Нет течи охлаждающей воды на Металлизации':
            with open("Ночная проверка инженерии на Металлизации " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " Утечка охлаждающей воды в зоне Металлизации ОТСУТСВУЕТ ")
                )
            file.close()
            bot.reply_to(message,
                         ' Информация зафиксировано в  ' + hour + ':' + minute + ' по отсутствию утечек охлаждающей воды на оборудованиях Металлизации ')



        elif message.text == 'Есть звук травления на Металлизации':
            with open("Ночная проверка инженерии на Металлизации " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Металлизации обнаружено звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Металлизации есть звук травления воздуха. \n1. Сообщить ССО, '

                                                                                           'если травление воздуха происходит внутри оборудования. \n2. Сообщить дежурному от инженерной службы и сообщить ССО, если травление воздуха происходит в магистральной линии (до оборудования).   ')


        elif message.text == "Нет звука травления на Металлизации":
            with open("Ночная проверка инженерии на Металлизации " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Металлизации отсутствует звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Металлизации отсутствует травление воздуха')



        elif message.text == 'Кабель/эле-ика нарушена на Металлизации':
            with open("Ночная проверка инженерии на Металлизации " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Металлизации обнаружено повреждение электроники и/или кабеля  ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Металлизации обнаружено повреждение электроники и/или кабеля. \n1. Сообщить ССО, '

                                                                                           'если повреждение внутри оборудования. \n2. Сообщить дежурному электрику от инженерной службы и сообщить ССО, если повреждение находиться вне оборудования (до оборудования).   ')



        elif message.text == "Кабель/эле-ика НЕ нарушена на Металлизации":

            with open("Ночная проверка инженерии на Металлизации " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Металлизации отсутствует повреждение электроники и/или кабеля ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Металлизации отсутствует повреждение электроники и/или кабеля')




        elif message.text == 'Есть звук травления на Фотоотджиге':
            with open("Ночная проверка инженерии на Фотоотджиге " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Фотоотджига обнаружено звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Фотоотджига есть звук травления воздуха. \n1. Сообщить ССО, '

                                                                                           'если травление воздуха происходит внутри оборудования. \n2. Сообщить дежурному от инженерной службы и сообщить ССО, если травление воздуха происходит в магистральной линии (до оборудования).   ')


        elif message.text == "Нет звука травления на Фотоотджиге":
            with open("Ночная проверка инженерии на Фотоотджиге " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Фотоотджига отсутствует звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Фотоотджига отсутствует травление воздуха')




        elif message.text == 'Кабель/эле-ика нарушена на Фотоотджиге':
            with open("Ночная проверка инженерии на Фотоотджиге " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Фотоотджига обнаружено повреждение электроники и/или кабеля  ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Фотоотджига обнаружено повреждение электроники и/или кабеля. \n1. Сообщить ССО, '

                                                                                           'если повреждение внутри оборудования. \n2. Сообщить дежурному электрику от инженерной службы и сообщить ССО, если повреждение находиться вне оборудования (до оборудования).   ')



        elif message.text == "Кабель/эле-ика НЕ нарушена на Фотоотджиге":

            with open("Ночная проверка инженерии на Фотоотджиге " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне Фотоотджига отсутствует повреждение электроники и/или кабеля ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне Фотоотджига отсутствует повреждение электроники и/или кабеля')





        elif message.text == 'Есть звук травления воздуха в зоне CIS':
            with open("Ночная проверка инженерии на CIS " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне CIS обнаружено звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне CIS есть звук травления воздуха. \n1. Сообщить ССО, '

                                                                                           'если травление воздуха происходит внутри оборудования. \n2. Сообщить дежурному от инженерной службы и сообщить ССО, если травление воздуха происходит в магистральной линии (до оборудования).   ')


        elif message.text == "Нет звука травления воздуха в зоне CIS":
            with open("Ночная проверка инженерии на CIS " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне CIS отсутствует звук травления воздуха ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне CIS отсутствует травление воздуха')




        elif message.text == 'Кабель нарушен в зоне CIS':
            with open("Ночная проверка инженерии на CIS " + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне CIS обнаружено повреждение электроники и/или кабеля  ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне CIS обнаружено повреждение электроники и/или кабеля. \n1. Сообщить ССО, '

                                                                                           'если повреждение внутри оборудования. \n2. Сообщить дежурному электрику от инженерной службы и сообщить ССО, если повреждение находиться вне оборудования (до оборудования).   ')



        elif message.text == "Кабель НЕ нарушен в зоне CIS":

            with open("Ночная проверка инженерии на CIS s" + last_day + "." + month + "." + year + ".csv", "a") as file:
                writer = csv.writer(file)
                writer.writerow(
                    (time.ctime(seconds), " В зоне CIS отсутствует повреждение электроники и/или кабеля ")
                )
            file.close()
            bot.reply_to(message,
                         'Информация зафиксировано, что на время ' + hour + ':' + minute + ' в зоне CIS отсутствует повреждение электроники и/или кабеля')



bot.polling(none_stop=True)
