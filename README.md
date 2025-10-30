
                    ]
        static void Main()
        {
            Application.EnableVisualStyles();
            Application.SetCompatibleTextRenderingDefault(false);
            Application.Run(new Form1());
        }
    }
}



using System;
using System.Drawing;
using System.Windows.Forms;

namespace CalculationApp
{
    public class Form1 : Form
    {
        private TextBox txtX;
        private TextBox txtY;
        private TextBox txtZ;
        private Label lblResultA;
        private Label lblResultB;

        public Form1()
        {
            InitializeComponent();
        }

        private void InitializeComponent()
        {
            // Настройка формы
            this.Text = "Вычисление a и b (вариант в)";
            this.ClientSize = new Size(300, 250);
            this.StartPosition = FormStartPosition.CenterScreen;
            
            // Создание элементов управления
            Label lblX = new Label();
            lblX.Text = "X:";
            lblX.Location = new Point(20, 20);
            lblX.AutoSize = true;
            
            txtX = new TextBox();
            txtX.Location = new Point(50, 17);
            txtX.Size = new Size(100, 20);
            txtX.Text = "1";
            
            Label lblY = new Label();
            lblY.Text = "Y:";
            lblY.Location = new Point(20, 50);
            lblY.AutoSize = true;
            
            txtY = new TextBox();
            txtY.Location = new Point(50, 47);
            txtY.Size = new Size(100, 20);
            txtY.Text = "2";
            
            Label lblZ = new Label();
            lblZ.Text = "Z:";
            lblZ.Location = new Point(20, 80);
            lblZ.AutoSize = true;
            
            txtZ = new TextBox();
            txtZ.Location = new Point(50, 77);
            txtZ.Size = new Size(100, 20);
            txtZ.Text = "3";
            
            Button btnCalc = new Button();
            btnCalc.Text = "Вычислить";
            btnCalc.Location = new Point(50, 110);
            btnCalc.Size = new Size(100, 30);
            btnCalc.Click += new EventHandler(BtnCalc_Click);
            
            lblResultA = new Label();
            lblResultA.Location = new Point(20, 160);
            lblResultA.AutoSize = true;
            lblResultA.Text = "a = ";
            
            lblResultB = new Label();
            lblResultB.Location = new Point(20, 185);
            lblResultB.AutoSize = true;
            lblResultB.Text = "b = ";
            
            // Добавление элементов на форму
            this.Controls.Add(lblX);
            this.Controls.Add(txtX);
            this.Controls.Add(lblY);
            this.Controls.Add(txtY);
            this.Controls.Add(lblZ);
            this.Controls.Add(txtZ);
            this.Controls.Add(btnCalc);
            this.Controls.Add(lblResultA);
            this.Controls.Add(lblResultB);
        }

        private void BtnCalc_Click(object sender, EventArgs e)
        {
            try
            {
                double x = double.Parse(txtX.Text);
                double y = double.Parse(txtY.Text);
                double z = double.Parse(txtZ.Text);

                // Вычисление a по формуле варианта "в"
                double denominatorA = Math.Exp(-x - 2) + 1.0 / (x * x + 4);
                double numeratorA = (1 + y) * (x + y / (x * x + 4));
                double a = numeratorA / denominatorA;

                // Вычисление b по формуле варианта "в"
                double denominatorB = (x * x * x * x) / 2.0 + Math.Sin(z) * Math.Sin(z);
                double numeratorB = 1 + Math.Cos(y - 2);
                double b = numeratorB / denominatorB;

                lblResultA.Text = string.Format("a = {0:F6}", a);
                lblResultB.Text = string.Format("b = {0:F6}", b);
            }
            catch (Exception ex)
            {
                MessageBox.Show("Ошибка: " + ex.Message, "Ошибка", 
                    MessageBoxButtons.OK, MessageBoxIcon.Error);
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
}
