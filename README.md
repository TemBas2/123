using System;
using System.Windows.Forms;

public partial class Form1 : Form
{
    private TextBox txtX = new TextBox();
    private TextBox txtY = new TextBox();
    private TextBox txtZ = new TextBox();
    private Button btnCalc = new Button();
    private Label lblA = new Label();
    private Label lblB = new Label();

    public Form1()
    {
        InitializeComponent();
    }

    private void InitializeComponent()
    {
        // Настройка формы
        this.Text = "Вычисление a и b";
        this.Size = new System.Drawing.Size(250, 200);
        
        // Позиционирование элементов
        txtX.Location = new System.Drawing.Point(50, 20);
        txtY.Location = new System.Drawing.Point(50, 50);
        txtZ.Location = new System.Drawing.Point(50, 80);
        btnCalc.Location = new System.Drawing.Point(50, 110);
        lblA.Location = new System.Drawing.Point(50, 140);
        lblB.Location = new System.Drawing.Point(50, 160);
        
        // Текст элементов
        btnCalc.Text = "Вычислить";
        
        // Добавление элементов на форму
        this.Controls.AddRange(new Control[] {
            new Label() { Text = "X:", Location = new System.Drawing.Point(20, 20) },
            txtX,
            new Label() { Text = "Y:", Location = new System.Drawing.Point(20, 50) },
            txtY,
            new Label() { Text = "Z:", Location = new System.Drawing.Point(20, 80) },
            txtZ,
            btnCalc,
            lblA,
            lblB
        });
        
        // Обработчик события
        btnCalc.Click += BtnCalc_Click;
    }

    private void BtnCalc_Click(object sender, EventArgs e)
    {
        try
        {
            double x = double.Parse(txtX.Text);
            double y = double.Parse(txtY.Text);
            double z = double.Parse(txtZ.Text);

            // Вычисление a
            double denominatorA = Math.Exp(-x - 2) + 1.0 / (x * x + 4);
            double numeratorA = (1 + y) * (x + y / (x * x + 4));
            double a = numeratorA / denominatorA;

            // Вычисление b
            double denominatorB = (x * x * x * x) / 2.0 + Math.Sin(z) * Math.Sin(z);
            double numeratorB = 1 + Math.Cos(y - 2);
            double b = numeratorB / denominatorB;

            lblA.Text = $"a = {a:F4}";
            lblB.Text = $"b = {b:F4}";
        }
        catch
        {
            MessageBox.Show("Ошибка ввода");
        }
    }

    [STAThread]
    static void Main()
    {
        Application.EnableVisualStyles();
        Application.Run(new Form1());
    }
}













using System;
using System.Drawing;
using System.Windows.Forms;

namespace CalculationApp
{
    public partial class Form1 : Form
    {
        private TextBox txtX, txtY, txtZ;
        private Label lblResultA, lblResultB;

        public Form1()
        {
            InitializeComponent();
        }

        private void InitializeComponent()
        {
            // Настройка формы
            this.Text = "Вычисление a и b (вариант в)";
            this.Size = new Size(300, 250);
            this.StartPosition = FormStartPosition.CenterScreen;
            
            // Создание элементов управления
            var lblX = new Label { Text = "X:", Location = new Point(20, 20), AutoSize = true };
            txtX = new TextBox { Location = new Point(50, 17), Size = new Size(100, 20), Text = "1" };
            
            var lblY = new Label { Text = "Y:", Location = new Point(20, 50), AutoSize = true };
            txtY = new TextBox { Location = new Point(50, 47), Size = new Size(100, 20), Text = "2" };
            
            var lblZ = new Label { Text = "Z:", Location = new Point(20, 80), AutoSize = true };
            txtZ = new TextBox { Location = new Point(50, 77), Size = new Size(100, 20), Text = "3" };
            
            var btnCalc = new Button { 
                Text = "Вычислить", 
                Location = new Point(50, 110),
                Size = new Size(100, 30)
            };
            btnCalc.Click += BtnCalc_Click;
            
            lblResultA = new Label { Location = new Point(20, 160), AutoSize = true, Text = "a = " };
            lblResultB = new Label { Location = new Point(20, 185), AutoSize = true, Text = "b = " };
            
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

                lblResultA.Text = $"a = {a:F6}";
                lblResultB.Text = $"b = {b:F6}";
            }
            catch (Exception ex)
            {
                MessageBox.Show($"Ошибка: {ex.Message}", "Ошибка", 
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
