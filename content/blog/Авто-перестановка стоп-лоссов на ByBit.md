+++
title = "Авто-перестановка стоп-лоссов на ByBit"
date = 2025-06-24
+++

Благодаря технологическим фичам байбита можно делать интересные штуки не беспокоясь о потери денег в случае чего.

На байбите есть Conditional Order. С помощью него можно выставить ордер при касании цены. Мой типичный кейс:

**1** - Я предполагаю что цена пойдет вверх и хочу войти, но не сейчас, а когда цена дойдет до определенного значения.

**2** - Также я не хочу входить тупо по рынку - это не очень приятно когда вход получается сильно выше. А такое бывает на большой волотильности. Потому я хочу установить лимит цены выше которого я не куплю. Тем более цена часто ходит туда-сюда, так что зачем покупать дорого если можно подождать пару минут.

**3** - Также я хочу поставить стоп-лосс чтобы не потерять больше чем могу себе позволить, ну а если всё хорошо - хочу чтобы сделка закрылась в плюс по указанной цене.

**4** - И самое главное - если цена дошла до нужного значения я хочу чтобы стоп передвинулся на точку безубыточности. И тогда я либо потеряю только оплату комиссий и не более того, либо заработаю полный капитал.

**5** - Ну и бонусом - я не хочу чтобы меня закрыло с убытком случайной флуктуацией фьючерса, а там бывает что цена ходит вне реальной цены. Аналогично и с ценой входа - хочется входить по реальной цене, а то всякое бывает. Зато вот для профита наоборот хорошо - может прострелить дальше и я получу прибыль даже если реальная цена актива туда не ходила, удобно.

И всё это решается двумя ордерами.

**Первый** - ставится Conditional Order. Цена касания (trigger price) ставится с пометкой index - сработает по реальной цене актива. Цена входа (price) ставится как максимальная приемлимая цена для входа, то есть купим не дороже указанного. Далее ставятся настройки цены стопа и тейка. И стоп ставится с пометкой index, а тейк с last - в итоге стоп по реальной, а тейк как долетит. И там есть настройка типа стопа/тейка - на всю позицию или на ордер. Выбирается на всю.

**Второй** - тоже Conditional Order, но с нюансом. Триггер ставится по цене где хочется перейти в безубыток, прайс - чуть ниже. Объем (quantity) - минимально допустимый для биржи. Задача этого ордера не купить ещё, а сделать финт, про который будет дальше. В настройке стопа/тейка на не нужен тейк - он произойдет вместе с основным, ведь в предыдущем ордере мы поставили настройку на всю позицию. А вот стоп ставим на цену входа (price) первого ордера (или выше, если хочется). И настройку типа стопа - на всю позицию. В итоге при срабатывании этого ордера купится минимальное количество и выставится новый стоп. И если он сработает - закроется вся позиция по указанной цене, а другие ордера отменятся. То что нужно!

Вот таким хитрым образом под гарантией исполнения от биржи мы спокойно можем передвигать стопы и не беспокоится о том что там сейчас на рынке.