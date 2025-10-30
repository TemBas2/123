using System;
using System.Drawing;
using System.Windows.Forms;

namespace WindowsForm4Api
{
    public class Form1 : Form
    {
        private TextBox textBoxX;
        private TextBox textBoxY;
        private TextBox textBoxZ;
        private Label labelResultA;
        private Label labelResultB;
        private Button buttonCalculate;

        public Form1()
        {
            InitializeComponent();
        }

        private void InitializeComponent()
        {
            // Настройка формы
            this.Text = "Задача 11в - Вычисление a и b";
            this.ClientSize = new Size(350, 250);
            this.StartPosition = FormStartPosition.CenterScreen;

            // Поля ввода
            Label labelX = new Label();
            labelX.Text = "X:";
            labelX.Location = new Point(20, 20);
            labelX.AutoSize = true;

            textBoxX = new TextBox();
            textBoxX.Location = new Point(50, 17);
            textBoxX.Size = new Size(80, 20);
            textBoxX.Text = "1";

            Label labelY = new Label();
            labelY.Text = "Y:";
            labelY.Location = new Point(150, 20);
            labelY.AutoSize = true;

            textBoxY = new TextBox();
            textBoxY.Location = new Point(180, 17);
            textBoxY.Size = new Size(80, 20);
            textBoxY.Text = "2";

            Label labelZ = new Label();
            labelZ.Text = "Z:";
            labelZ.Location = new Point(280, 20);
            labelZ.AutoSize = true;

            textBoxZ = new TextBox();
            textBoxZ.Location = new Point(310, 17);
            textBoxZ.Size = new Size(80, 20);
            textBoxZ.Text = "3";

            // Кнопка вычисления
            buttonCalculate = new Button();
            buttonCalculate.Text = "Вычислить";
            buttonCalculate.Location = new Point(20, 60);
            buttonCalculate.Size = new Size(100, 30);
            buttonCalculate.Click += ButtonCalculate_Click;

            // Метки результатов
            labelResultA = new Label();
            labelResultA.Location = new Point(20, 110);
            labelResultA.AutoSize = true;
            labelResultA.Text = "a = ";

            labelResultB = new Label();
            labelResultB.Location = new Point(20, 140);
            labelResultB.AutoSize = true;
            labelResultB.Text = "b = ";

            // Добавление элементов на форму
            this.Controls.Add(labelX);
            this.Controls.Add(textBoxX);
            this.Controls.Add(labelY);
            this.Controls.Add(textBoxY);
            this.Controls.Add(labelZ);
            this.Controls.Add(textBoxZ);
            this.Controls.Add(buttonCalculate);
            this.Controls.Add(labelResultA);
            this.Controls.Add(labelResultB);
        }

        private void ButtonCalculate_Click(object sender, EventArgs e)
        {
            double x = double.Parse(textBoxX.Text);
            double y = double.Parse(textBoxY.Text);
            double z = double.Parse(textBoxZ.Text);

            // Вычисление a
            double denominatorA = Math.Exp(-x - 2) + 1.0 / (x * x + 4);
            double numeratorA = (1 + y) * (x + y / (x * x + 4));
            double a = numeratorA / denominatorA;

            // Вычисление b
            double denominatorB = (x * x * x * x) / 2.0 + Math.Sin(z) * Math.Sin(z);
            double numeratorB = 1 + Math.Cos(y - 2);
            double b = numeratorB / denominatorB;

            labelResultA.Text = "a = " + a.ToString("F6");
            labelResultB.Text = "b = " + b.ToString("F6");
        }
    }

    internal static class Program
    {
        [STAThread]
        static void Main()
        {
            Application.EnableVisualStyles();
            Application.SetCompatibleTextRenderingDefault(false);
            Application.Run(new Form1());
        }
    }
}
