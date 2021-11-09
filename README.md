# C-Users-1-PycharmProjects-pythonProject1
import random
import logging
import requests
import json

from telegram.ext import Updater, CommandHandler, MessageHandler, Filters
from telegram import Update


BOT_API_TOKEN = '2059684982:AAEiC9KhZ02L5oKCRFr5G7os5emyP3wnrhE'
HELP_COMMAND = ' Привет, мой дорогой пользователь! Вот список всех команд и действий,' \
               ' которые ты можешь во мне потыкать.\n'\
                '/help\n/start\n'
CAT_URL = 'https://api.thecatapi.com/v1/images/search'
NEWS_API_KEY = '5a9a2b504d37442a93e1be46727c96f6'
NEWS_URL = f'https://newsapi.org/v2/top-headlines?country=ru&apiKey={NEWS_API_KEY}'




def start(update: Update, context) -> None:
    update.message.reply_text('бот стартует, иуууу')

def get_cat(update: Update, context) -> None:
    req = requests.get(CAT_URL)

    if req.status_code == 200:
        req_text = req.text
        req_dict = json.loads(req_text)[0]
        result = req_dict['url']
    else:
        result = 'Запрос не удался :('

    update.message.reply_text(result)


def help(update: Update, context) -> None:
    update.message.reply_text('Оу оу оу, загадочный гость, наш бот умеет:\n' \
                 '1. Калькулятор, для того чтобы им воспользоваться надо написать: /calculate_(ваш пример)..\n ' \
                 '2. Также наш бот хоть немного, но умеет говорить и отвечать на ваши вопросы, он ещё маленький, развивается..\n'
                 '3. Также если вам срочно нужна таблица Менделеева, обращайтесть к нам, бот сразу же вам скажет атомный номер и переведёт на латынь\n'
                 '(реклама как у LEOMAX ей-богу..)')


def random_news(update: Update, context) -> None:
    req = requests.get(NEWS_URL)
    print(req.text)
    if req.status_code == 200:
        req_text = req.text
        data = json.loads(req_text)
        list_of_news = data['articles']
        random_news_dict = random.choice(list_of_news)
        title = random_news_dict['title']
        description = random_news_dict['description']
        url = random_news_dict['url']
        source_name = random_news_dict['source']['name']
        result = f'Заголовок: {title}\n\nИсточник: {source_name}\n\n{description}\n\nСсылка: {url}'
    else:
        result = 'Запрос к API не удался :('

    update.message.reply_text(result)

def message_handler(update: Update, context) -> None:
    message = update.message.text.lower()
    result = ''

    if '/calculate_' in message:
        expr = message.split('_')[1]  # ['/calculate', 'asdasdas']
        try:
            if '+' in expr:
                list_of_nums = list(map(lambda x: int(x), expr.split('+')))  # [1, 5]
                result = str(sum(list_of_nums))  # '6'
            elif '-' in expr:
                list_of_nums = list(map(lambda x: int(x), expr.split('-')))  # [1, 5]
                print(list_of_nums)
                result = str(list_of_nums[0] - list_of_nums[1])
            elif '*' in expr:
                list_of_nums = list(map(lambda x: int(x), expr.split('*')))  # [1, 5]
                print(list_of_nums)
                result = str(list_of_nums[0] * list_of_nums[1])
            elif '/' in expr:
                list_of_nums = list(map(lambda x: int(x), expr.split('/')))  # [1, 5]
                print(list_of_nums)
                try:
                    result = str(list_of_nums[0] / list_of_nums[1])
                except ZeroDivisionError:
                    result = 'иди учи математику!!!'
            else:
                result = 'Выражение не составлено'
        except ValueError:
            result = 'Выражение составлено некорректно'
    elif 'прив' in message:
        result = 'Ола '
    elif 'пок' in message:
        result = 'аривидерчи'
    elif 'как дела' in message:
        result = 'волшебно, у тебя как?и'
    elif 'что делаешь' in message:
        result = 'да так, ничего'
    elif 'скажи мне какой-нибудь комплитмен' in message:
        result = 'у тебя глаза краисвые..'
    elif 'салам' in message:
        result = 'салам пополам '
    elif 'хорошо' in message:
        result = 'оууу, я рад за тебя '
    elif 'отлично' in message:
        result = 'оууу, я рад за тебя '
    elif 'не оч' in message:
        result = 'эйй, ну ты чего..?'
    elif 'водород' in message:
        result = 'H(1)'
    elif 'литий' in message:
        result = 'Li(3)'
    elif 'берилий' in message:
        result = 'Be(4)'
    elif 'бор' in message:
        result = 'B(5)'
    elif 'углерод' in message:
        result = 'C(6)'
    elif 'азот' in message:
        result = 'N(7)'
    elif 'кислород' in message:
        result = 'O(8)'
    elif 'фтор' in message:
        result = 'F(9)'
    elif 'неон' in message:
        result = 'Ne(10)'
    elif 'натрий' in message:
        result = 'Na(11)'
    elif 'магний' in message:
        result = 'Mg(12)'
    elif 'алюминий' in message:
        result = 'Al(13)'
    elif 'кремний' in message:
        result = 'Si(14)'
    elif 'фосфор' in message:
        result = 'P(15)'
    elif 'сера' in message:
        result = 'S(16)'
    elif 'хлор' in message:
        result = 'Cl(17)'
    elif 'аргон' in message:
        result = 'Ar(18)'
    elif 'калий' in message:
        result = 'K(19)'
    elif 'кальций' in message:
        result = 'Ca(20)'
    elif 'скандий' in message:
        result = 'Sc(21)'
    elif 'титан' in message:
        result = 'Ti(22)'
    elif 'ванадий' in message:
        result = 'V(23)'
    elif 'хром' in message:
        result = 'Cr(24)'
    elif 'марганец' in message:
        result = 'Mn(25)'
    elif 'железо' in message:
        result = 'Fe(26)'
    elif 'кобальт' in message:
        result = 'Co(27)'
    elif 'никель' in message:
        result = 'Ni(28)'
    elif 'медь' in message:
        result = 'Cu(29)'
    elif 'цинк' in message:
        result = 'Zn(30)'
    elif 'галлий' in message:
        result = 'Ga(31)'
    elif 'германий' in message:
        result = 'Ge(32)'
    elif 'мышьяк' in message:
        result = 'As(33)'
    elif 'селен' in message:
        result = 'Se(34)'
    elif 'бром' in message:
        result = 'Br(35)'
    elif 'криптон' in message:
        result = 'Kr(36)'
    elif 'рубидий' in message:
        result = 'Rb(37)'
    elif 'строниций' in message:
        result = 'Sr(38)'
    elif 'иттрий' in message:
        result = 'Y(39)'
    elif 'цирконий' in message:
        result = 'Zr(40)'
    elif 'ниобий' in message:
        result = 'Nb(41)'
    elif 'молибден' in message:
        result = 'Mo(42)'
    elif 'технецкий' in message:
        result = 'Tc(43)'
    elif 'рутений' in message:
        result = 'Ru(44)'
    elif 'родий' in message:
        result = 'Rh(45)'
    elif 'палладий' in message:
        result = 'Pd(46)'
    elif 'серебро' in message:
        result = 'Ag(47)'
    elif 'кадмий' in message:
        result = 'Cd(48)'
    elif 'индий' in message:
        result = 'In(49)'
    elif 'олово' in message:
        result = 'Sn(50)'
    elif 'сурьма' in message:
        result = 'Sb(51)'
    elif 'теллур' in message:
        result = 'Te(52)'
    elif 'йод' in message:
        result = 'I(53)'
    elif 'ксенон' in message:
        result = 'Xe(54)'
    elif 'цезий' in message:
        result = 'Cs(55)'
    elif 'барий' in message:
        result = 'Ba(56)'
    elif 'лантан' in message:
        result = 'La(57)'
    elif 'гафний' in message:
        result = 'Hf(72)'
    elif 'тантал' in message:
        result = 'Ta(73)'
    elif 'вольфрам' in message:
        result = 'W(74)'
    elif 'рений' in message:
        result = 'Re(75)'
    elif 'осмий' in message:
        result = 'Os(76)'
    elif 'иридий' in message:
        result = 'Ir(77)'
    elif 'платина' in message:
        result = 'Pt(78)'
    elif 'золото' in message:
        result = 'Au(79)'
    elif 'ртуть' in message:
        result = 'Hg(80)'
    elif 'таллий' in message:
        result = 'Tl(81)'
    elif 'свинец' in message:
        result = 'Pb(82)'
    elif 'висмут' in message:
        result = 'Bi(83)'
    elif 'полоний' in message:
        result = 'Po(84)'
    elif 'астат' in message:
        result = 'At(85)'
    elif 'радон' in message:
        result = 'Rn(86)'
    elif 'франций' in message:
        result = 'Fr(87)'
    elif 'радий' in message:
        result = 'Ra(88)'
    elif 'актиний' in message:
        result = 'Ac(89)'
    elif 'резерфордий' in message:
        result = 'Rf(104)'
    elif 'дубний' in message:
        result = 'Db(105)'
    elif 'сиборгий' in message:
        result = 'Sg(106)'
    elif 'борий' in message:
        result = 'Bh(107)'
    elif 'хассий' in message:
        result = 'Hs(108)'
    elif 'мейтнерий' in message:
        result = 'Mt(109)'
    elif 'дармштадтий' in message:
        result = 'Ds(110)'
    elif 'рентгений' in message:
        result = 'Rg(111)'
    elif 'коперницей' in message:
        result = 'Cn(112)'
    elif 'нихоний' in message:
        result = 'Nh(113)'
    elif 'флеровий' in message:
        result = 'Fl(114)'
    elif 'московий' in message:
        result = 'Mc(115)'
    elif 'ливермортий' in message:
        result = 'Lv(116)'
    elif 'теннесин' in message:
        result = 'Ts(117)'
    elif 'оганесон' in message:
        result = 'Og(118)'
    
    else:
        result = 'Я не знаю что тебе ответить :('

    update.message.reply_text(result)


def main() -> None:
    logging.basicConfig(
        level=logging.DEBUG,
        format='%(asctime)s - %(name)s - %(levelname)s - %(message)s'
    )

    updater = Updater(BOT_API_TOKEN, use_context=True)
    dispatcher = updater.dispatcher

    dispatcher.add_handler(CommandHandler('start', start))
    dispatcher.add_handler(CommandHandler('help', help))
    dispatcher.add_handler(CommandHandler('random_news', random_news))
    dispatcher.add_handler(CommandHandler('get_cat', get_cat))
    dispatcher.add_handler(MessageHandler(Filters.text, message_handler))



    updater.start_polling()
    updater.help_polling()
    updater.idle()
if __name__ == '__main__':
    main()

