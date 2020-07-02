# sem4-t2
Тема 2. Декораторы
## Декоратор 1 (встроенный в язык)
Данный декоратор позволяет делать метод класса статичным - т.е вызов этого метода может совершаться без инстанцирования класса
```python
@staticmethod
    def get_first_case_score(goals, side, side_map, low):
        if side == 'rus':
            return int(sum(
                [side_map[side][0][i] * (goals[i] - low) / (side_map[side][1][i] - low) for i in range(0, len(goals))]))
        elif side == 'china':
            return int(sum(
                [side_map[side][0][i] * (side_map[side][1][i] - goals[i]) / (side_map[side][1][i] - low) for i in
                 range(0, len(goals))]))
```
## Декоратор 2
Декоратор из библиотеки telebot позволяющий осуществлять фильтрацию сообщений приходящих боту
@bot.message_handler(content_types='voice')
def handle_voice(message):
    if message.chat.id in dispatcher.users_list():
        ctrl.update_voice_counter(message.chat.id)
        cur_user = dispatcher.users()[message.chat.id]
        print('ID = {0}; message = {1}'.format(message.chat.id, message.text))
        VS.download_voice(message, cur_user.id, cur_user.name(), cur_user.surname(), True)
        cur_user.handler(message)
    else:
        dispatcher.add_user(message.chat.id, bot, ctrl, message, test_one)
        print(dispatcher.users_list())
