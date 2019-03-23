using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using MySql.Data.MySqlClient;

namespace WindowsFormsApp5
{
    public partial class Form1 : Form
    {
        MySqlConnection MySqlConnection;
        MySqlCommand MySqlCommand;
        MySqlDataReader reader;
        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            cargardatos();

        }
        private void cargardatos()
        {
            try
            {
                
                MySqlConnection = new
               MySqlConnection("host=localhost;user=root;password=1234;database=punto_de_venta");
                MySqlConnection.Open();
                MySqlCommand = new MySqlCommand("SELECT * FROM productos",
               MySqlConnection);
                reader = MySqlCommand.ExecuteReader();
                while (reader.Read())
                {
                    dataGridView1.Rows.Add(reader.GetString(0),
                   (reader.GetString(1)), (reader.GetString(2)), (reader.GetString(3)));
                }
                MySqlConnection.Close();
            }
            catch (Exception error)
            {
                MessageBox.Show(error.ToString());
            }

        }
    }
}
