using System;
using System.Drawing;
using System.Windows.Forms;

namespace Task11v
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
            this.ClientSize = new Size(350, 300);
            this.StartPosition = FormStartPosition.CenterScreen;
            this.Font = new Font("Microsoft Sans Serif", 10F, FontStyle.Regular, GraphicsUnit.Point, ((byte)(204)));

            // Заголовок
            Label labelTitle = new Label();
            labelTitle.Text = "Вычисление значений a и b по формулам:";
            labelTitle.Location = new Point(20, 20);
            labelTitle.AutoSize = true;
            labelTitle.Font = new Font(this.Font, FontStyle.Bold);

            Label labelFormulaA = new Label();
            labelFormulaA.Text = "a = (1 + y) * (x + y/(x² + 4)) / (e^(-x-2) + 1/(x² + 4))";
            labelFormulaA.Location = new Point(20, 50);
            labelFormulaA.AutoSize = true;

            Label labelFormulaB = new Label();
            labelFormulaB.Text = "b = (1 + cos(y-2)) / (x⁴/2 + sin²(z))";
            labelFormulaB.Location = new Point(20, 75);
            labelFormulaB.AutoSize = true;

            // Поля ввода
            Label labelX = new Label();
            labelX.Text = "X:";
            labelX.Location = new Point(20, 120);
            labelX.AutoSize = true;

            textBoxX = new TextBox();
            textBoxX.Location = new Point(50, 117);
            textBoxX.Size = new Size(80, 23);
            textBoxX.Text = "1";

            Label labelY = new Label();
            labelY.Text = "Y:";
            labelY.Location = new Point(150, 120);
            labelY.AutoSize = true;

            textBoxY = new TextBox();
            textBoxY.Location = new Point(180, 117);
            textBoxY.Size = new Size(80, 23);
            textBoxY.Text = "2";

            Label labelZ = new Label();
            labelZ.Text = "Z:";
            labelZ.Location = new Point(280, 120);
            labelZ.AutoSize = true;

            textBoxZ = new TextBox();
            textBoxZ.Location = new Point(310, 117);
            textBoxZ.Size = new Size(80, 23);
            textBoxZ.Text = "3";

            // Кнопка вычисления
            buttonCalculate = new Button();
            buttonCalculate.Text = "Вычислить";
            buttonCalculate.Location = new Point(20, 160);
            buttonCalculate.Size = new Size(100, 30);
            buttonCalculate.Click += new EventHandler(ButtonCalculate_Click);

            // Метки результатов
            labelResultA = new Label();
            labelResultA.Location = new Point(20, 210);
            labelResultA.AutoSize = true;
            labelResultA.Text = "a = ";

            labelResultB = new Label();
            labelResultB.Location = new Point(20, 240);
            labelResultB.AutoSize = true;
            labelResultB.Text = "b = ";

            // Добавление элементов на форму
            this.Controls.Add(labelTitle);
            this.Controls.Add(labelFormulaA);
            this.Controls.Add(labelFormulaB);
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
            try
            {
                // Чтение введенных значений
                double x = double.Parse(textBoxX.Text);
                double y = double.Parse(textBoxY.Text);
                double z = double.Parse(textBoxZ.Text);

                // Вычисление значения a
                // a = (1 + y) * (x + y/(x² + 4)) / (e^(-x-2) + 1/(x² + 4))
                double denominatorA = Math.Exp(-x - 2) + 1.0 / (x * x + 4);
                
                // Проверка деления на ноль
                if (Math.Abs(denominatorA) < 1e-15)
                {
                    labelResultA.Text = "a = ошибка (деление на ноль)";
                    labelResultB.Text = "b = ";
                    return;
                }
                
                double numeratorA = (1 + y) * (x + y / (x * x + 4));
                double a = numeratorA / denominatorA;

                // Вычисление значения b
                // b = (1 + cos(y-2)) / (x⁴/2 + sin²(z))
                double denominatorB = (x * x * x * x) / 2.0 + Math.Sin(z) * Math.Sin(z);
                
                // Проверка деления на ноль
                if (Math.Abs(denominatorB) < 1e-15)
                {
                    labelResultA.Text = string.Format("a = {0:F6}", a);
                    labelResultB.Text = "b = ошибка (деление на ноль)";
                    return;
                }

                double numeratorB = 1 + Math.Cos(y - 2);
                double b = numeratorB / denominatorB;

                // Вывод результатов
                labelResultA.Text = string.Format("a = {0:F6}", a);
                labelResultB.Text = string.Format("b = {0:F6}", b);
            }
            catch (FormatException)
            {
                MessageBox.Show("Ошибка ввода. Пожалуйста, введите корректные числовые значения для X, Y и Z.", 
                              "Ошибка ввода", MessageBoxButtons.OK, MessageBoxIcon.Error);
            }
            catch (OverflowException)
            {
                MessageBox.Show("Ошибка: введено слишком большое или слишком маленькое число.", 
                              "Ошибка", MessageBoxButtons.OK, MessageBoxIcon.Error);
            }
            catch (Exception ex)
            {
                MessageBox.Show("Произошла ошибка: " + ex.Message, 
                              "Ошибка", MessageBoxButtons.OK, MessageBoxIcon.Error);
            }
        }

        [STAThread]
        static void Main()
        {
            Application.EnableVisualStyles();
            Application.SetCompatibleTextRenderingDefault(false);
            Application.Run(new Form1());
        }
    }

    // Класс Program не нужен - точка входа находится в Form1
}
