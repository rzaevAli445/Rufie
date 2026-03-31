from kivy.app import App
from kivy.uix.screenmanager import ScreenManager, Screen
from kivy.uix.boxlayout import BoxLayout
from kivy.uix.label import Label
from kivy.uix.button import Button
from kivy.uix.textinput import TextInput
from instructions import txt_instruction, txt_test1, txt_test3, txt_sits


def ruffier_index(P1, P2, P3):
    S = 4 * (P1 + P2 + P3)
    Th = (S - 200) / 10
    return Th


class InstrScr(Screen):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.name = 'instr'

        instr = Label(text=txt_instruction)
        lbl1 = Label(text='Введите имя:')
        self.in_name = TextInput(multiline=False)

        lbl2 = Label(text='Введите возраст:')
        self.in_age = TextInput(multiline=False, input_filter='int')

        self.btn = Button(
            text='Начать',
            size_hint=(0.3, 0.2),
            pos_hint={'center_x': 0.5}
        )
        self.btn.bind(on_press=self.next)

        self.error_label = Label(text='', size_hint=(0.8, 0.1))

        line1 = BoxLayout(size_hint=(0.8, 0.1))
        line2 = BoxLayout(size_hint=(0.8, 0.1))

        line1.add_widget(lbl1)
        line1.add_widget(self.in_name)

        line2.add_widget(lbl2)
        line2.add_widget(self.in_age)

        outer = BoxLayout(orientation='vertical', padding=8, spacing=8)
        outer.add_widget(instr)
        outer.add_widget(line1)
        outer.add_widget(line2)
        outer.add_widget(self.error_label)
        outer.add_widget(self.btn)

        self.add_widget(outer)

    def next(self, button):
        if self.in_name.text.strip() == '':
            self.error_label.text = 'Ошибка ввода имени'
            return

        try:
            age = int(self.in_age.text)
        except ValueError:
            self.error_label.text = 'Ошибка ввода возраста'
            return

        app = App.get_running_app()
        app.user_data['name'] = self.in_name.text.strip()
        app.user_data['age'] = age

        self.error_label.text = ''
        self.manager.current = 'pulse1'


class PulseScr(Screen):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.name = 'pulse1'

        instr = Label(text=txt_test1)

        line = BoxLayout(size_hint=(0.8, 0.1))
        lbl_result = Label(text='Введите результат:')
        self.in_result = TextInput(multiline=False, input_filter='int')
        line.add_widget(lbl_result)
        line.add_widget(self.in_result)

        self.error_label = Label(text='', size_hint=(0.8, 0.1))

        self.btn = Button(
            text='Продолжить',
            size_hint=(0.3, 0.2),
            pos_hint={'center_x': 0.5}
        )
        self.btn.bind(on_press=self.next)

        outer = BoxLayout(orientation='vertical', padding=8, spacing=8)
        outer.add_widget(instr)
        outer.add_widget(line)
        outer.add_widget(self.error_label)
        outer.add_widget(self.btn)

        self.add_widget(outer)

    def next(self, button):
        try:
            p1 = int(self.in_result.text)
        except ValueError:
            self.error_label.text = 'Введите число'
            return

        app = App.get_running_app()
        app.user_data['p1'] = p1
        self.error_label.text = ''
        self.manager.current = 'sits'


class CheckSits(Screen):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.name = 'sits'

        instr = Label(text=txt_sits)

        self.btn = Button(
            text='Продолжить',
            size_hint=(0.3, 0.2),
            pos_hint={'center_x': 0.5}
        )
        self.btn.bind(on_press=self.next)

        outer = BoxLayout(orientation='vertical', padding=8, spacing=8)
        outer.add_widget(instr)
        outer.add_widget(self.btn)

        self.add_widget(outer)

    def next(self, button):
        self.manager.current = 'pulse2'


class PulseScr2(Screen):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.name = 'pulse2'

        instr = Label(text=txt_test3)

        line1 = BoxLayout(size_hint=(0.8, 0.1))
        lbl_result1 = Label(text='Результат:')
        self.in_result1 = TextInput(multiline=False, input_filter='int')
        line1.add_widget(lbl_result1)
        line1.add_widget(self.in_result1)

        line2 = BoxLayout(size_hint=(0.8, 0.1))
        lbl_result2 = Label(text='Результат после отдыха:')
        self.in_result2 = TextInput(multiline=False, input_filter='int')
        line2.add_widget(lbl_result2)
        line2.add_widget(self.in_result2)

        self.error_label = Label(text='', size_hint=(0.8, 0.1))

        self.btn = Button(
            text='Завершить',
            size_hint=(0.3, 0.2),
            pos_hint={'center_x': 0.5}
        )
        self.btn.bind(on_press=self.next)

        outer = BoxLayout(orientation='vertical', padding=8, spacing=8)
        outer.add_widget(instr)
        outer.add_widget(line1)
        outer.add_widget(line2)
        outer.add_widget(self.error_label)
        outer.add_widget(self.btn)

        self.add_widget(outer)

    def next(self, button):
        try:
            p2 = int(self.in_result1.text)
            p3 = int(self.in_result2.text)
        except ValueError:
            self.error_label.text = 'Введите числа в оба поля'
            return

        app = App.get_running_app()
        app.user_data['p2'] = p2
        app.user_data['p3'] = p3

        self.error_label.text = ''
        self.manager.current = 'result'


class Result(Screen):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.name = 'result'

        self.outer = BoxLayout(orientation='vertical', padding=8, spacing=8)
        self.instr = Label(text='Индекс Руфье: ')
        self.outer.add_widget(self.instr)
        self.add_widget(self.outer)

    def on_pre_enter(self, *args):
        app = App.get_running_app()
        p1 = app.user_data.get('p1', 0)
        p2 = app.user_data.get('p2', 0)
        p3 = app.user_data.get('p3', 0)

        result = ruffier_index(p1, p2, p3)
        self.instr.text = f'Индекс Руфье: {result:.2f}'


class HeartCheck(App):
    def build(self):
        self.user_data = {}

        sm = ScreenManager()
        sm.add_widget(InstrScr())
        sm.add_widget(PulseScr())
        sm.add_widget(CheckSits())
        sm.add_widget(PulseScr2())
        sm.add_widget(Result())

        return sm


app = HeartCheck()
app.run()
