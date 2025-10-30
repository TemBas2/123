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
