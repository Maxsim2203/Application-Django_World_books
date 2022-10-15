Приложение создано для администрации сайта проекта Мир книг.
Приложение состоит из форм:
1) Главной формы 
2) Авторизации
3) О программе 
4) Капчи
5) Вывода таблицы


1) Главная форма 

![image](https://user-images.githubusercontent.com/95234863/195976157-9d16fa20-ee35-40bc-b784-684b23105254.png)
 Код главной формы 
 '''
 namespace WinFormsApp1
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void button1_Click(object sender, EventArgs e)
        {
            Form2_info_programm f = new Form2_info_programm();
            f.Show();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
           
        }

        private void button3_Click(object sender, EventArgs e)
        {
            Form2_avtorization  f = new Form2_avtorization();
            f.Show();
        }
    }
}
 '''
 
 




