Приложение создано для администрации сайта проекта Мир книг.
Приложение состоит из форм:
1) Главной формы 
2) Авторизации
3) О программе 
4) Капчи
5) Вывода таблицы
   Данный readme описывает основные принципы приложения а также некоторые части кода 

1) Главная форма 

![image](https://user-images.githubusercontent.com/95234863/195976157-9d16fa20-ee35-40bc-b784-684b23105254.png)


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
    
    
 '''
 
  2) Авторизация
  ![image](https://user-images.githubusercontent.com/95234863/195976221-af2abd5f-fe93-4603-99bd-7a1f2648c3c2.png)


  '''
  
  using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace WinFormsApp1
{
    public partial class Form2_avtorization : Form
    {
        public Users[] user = new Users[]
        {
            new Users("admin", "123")
        };
        public Form2_avtorization()
        {
            InitializeComponent();
        }

        private void label1_Click(object sender, EventArgs e)
        {

        }

        private void textBox1_TextChanged(object sender, EventArgs e)
        {

        }

        private void button1_Click(object sender, EventArgs e)
        {
            this.Close();
        }

        private void button2_Click(object sender, EventArgs e)
        {
            for (int i = 0; i < user.Length; i++)
            {
                if (textBox1.Text == user[i].Login && textBox2.Text == user[i].Password)
                {
                Form_capcha f = new Form_capcha();
                f.Show();
                }
                else
                {
                    MessageBox.Show("Повторите попытку");
                }
            }
           
        }

        private void Form2_avtorization_Load(object sender, EventArgs e)
        {

        }

        private void label3_Click(object sender, EventArgs e)
        {

        }
    }
    
  '''
  
    '''
  
  using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace WinFormsApp1
{
    public partial class Form2_info_programm : Form
    {
        public Form2_info_programm()
        {
            InitializeComponent();
        }

        private void Form2_info_programm_Load(object sender, EventArgs e)
        {

        }

        private void button1_Click(object sender, EventArgs e)
        {
            this.Close();
        }

        private void button2_Click(object sender, EventArgs e)
        {
            this.Close();
        }
    }
    
  '''
  
  4) Капча
  
  ![image](https://user-images.githubusercontent.com/95234863/195976346-e5ae68ba-b437-4cb1-b220-87a9ab28a70f.png)

  '''
  
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using static System.Net.Mime.MediaTypeNames;
using Image = System.Drawing.Image;

namespace WinFormsApp1
{
    public partial class Form_captcha : Form
    {
        public Form_captcha()
        {
            InitializeComponent();
        }
        public string text = String.Empty;


        private Bitmap CreateImage(int Width, int Height)
        {
            Random rnd = new Random();

            //Создадим изображение
            Bitmap result = new Bitmap(Width, Height);

            //Вычислим позицию текста
            int Xpos = 10;
            int Ypos = 10;

            //Добавим различные цвета ддя текста
            Brush[] colors = {
Brushes.Black,
Brushes.Red,
Brushes.RoyalBlue,
Brushes.Green,
Brushes.Yellow,
Brushes.White,
Brushes.Tomato,
Brushes.Sienna,
Brushes.Pink };

            //Добавим различные цвета линий
            Pen[] colorpens = {
Pens.Black,
Pens.Red,
Pens.RoyalBlue,
Pens.Green,
Pens.Yellow,
Pens.White,
Pens.Tomato,
Pens.Sienna,
Pens.Pink };

            //Делаем случайный стиль текста
            FontStyle[] fontstyle = {
FontStyle.Bold,
FontStyle.Italic,
FontStyle.Regular,
FontStyle.Strikeout,
FontStyle.Underline};

            //Добавим различные углы поворота текста
            Int16[] rotate = { 1, -1, 2, -2, 3, -3, 4, -4, 5, -5, 6, -6 };

            //Укажем где рисовать
            Graphics g = Graphics.FromImage((Image)result);

            //Пусть фон картинки будет серым
            g.Clear(Color.Gray);

            //Делаем случайный угол поворота текста
            g.RotateTransform(rnd.Next(rotate.Length));

            //Генерируем текст
             string ALF = "1234567890QWERTYUIOPASDFGHJKLZXCVBNM";
for (int i = 0; i < 5; ++i)
                text += ALF[rnd.Next(ALF.Length)];

            //Нарисуем сгенирируемый текст
            g.DrawString(text,
            new Font("Arial", 25, fontstyle[rnd.Next(fontstyle.Length)]),
            colors[rnd.Next(colors.Length)],
            new PointF(Xpos, Ypos));

            //Добавим немного помех
            //Линии из углов
            g.DrawLine(colorpens[rnd.Next(colorpens.Length)],
            new Point(0, 0),
            new Point(Width - 1, Height - 1));
            g.DrawLine(colorpens[rnd.Next(colorpens.Length)],
            new Point(0, Height - 1),
            new Point(Width - 1, 0));

            //Белые точки
            for (int i = 0; i < Width; ++i)
                for (int j = 0; j < Height; ++j)
                    if (rnd.Next() % 20 == 0)
                        result.SetPixel(i, j, Color.White);

            return result;
        }
        private void button2_Click(object sender, EventArgs e)
        {
            this.Close();
        }

        private void Form_captcha_Load(object sender, EventArgs e)
        {
            pictureBox1.Image = this.CreateImage(pictureBox1.Width, pictureBox1.Height);
        }

        private void button3_Click(object sender, EventArgs e)
        {
            pictureBox1.Image = this.CreateImage(pictureBox1.Width, pictureBox1.Height);
        }

        private void button1_Click(object sender, EventArgs e)
        {
            if (textBox1.Text == this.Text)
                MessageBox.Show("Верно!");

            else
                MessageBox.Show("Ошибка!");
        }
    }

  '''
  
  5) Форма вывода таблицы 
 
  ![image](https://user-images.githubusercontent.com/95234863/195976402-a684ead6-59f8-4c44-ab76-41d25cbd64ef.png)

  '''
  using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace WinFormsApp1
{
    public partial class Form_base : Form
    {
        public Form_base()
        {
            InitializeComponent();
        }

        private void dataGridView1_CellContentClick(object sender, DataGridViewCellEventArgs e)
        {

        }

        private void Form_base_Load(object sender, EventArgs e)
        {
            DB dataBase = new DB();
            dataBase.Display("SELECT id,\r\n       title,\r\n       summary,\r\n       isbn,\r\n       genre_id,\r\n       language_id\r\n  FROM catalog_book;\r\n", dataGridView1);
        }

        private void menuStrip1_ItemClicked(object sender, ToolStripItemClickedEventArgs e)
        {

        }
    }

  '''
  
  Так же для нормального вывода таблицы был создан класс 
  
  
  '''
  using System;
using System.Collections.Generic;
using System.Data.SQLite;
using System.Data;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace WinFormsApp1
{
    public  class DB
    {
        SQLiteConnection connection = new SQLiteConnection("Data Source=db.sqlite3;Version=3;");

        SQLiteConnection GetConnection()
        {
            return connection;
        }

        public void Display(string query, DataGridView dgv)
        {
            string sql = query;
            SQLiteConnection connection = GetConnection();
            SQLiteCommand command = new SQLiteCommand(sql, connection);
            SQLiteDataAdapter adapter = new SQLiteDataAdapter(command);
            DataTable dt = new DataTable();
            adapter.Fill(dt);
            dgv.DataSource = dt;
            connection.Close();
        }
    }

  '''
 
 
 
 




