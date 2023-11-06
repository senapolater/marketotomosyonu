# marketotomosyonu
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Data.SqlClient;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace MARKET_OTO
{
    public partial class ürünform : Form
    {

        SqlConnection crs = new SqlConnection
      ("Server=.;Database=MARKETOTO;Encrypt=False;Trusted_Connection=True;");
        public ürünform()
        {
            InitializeComponent();
        }

        private void btnEkle_Click(object sender, EventArgs e)
        {
            crs.Open();
            SqlCommand baglanti = new SqlCommand("insert into T_URUN(Adi,Aciklama,miktar) values('" + txtadi.Text + "','" + txtaciklama.Text + "','" + txtmiktar.Text + "')", crs);
            int son = baglanti.ExecuteNonQuery();
            if (son > 0)
            {
                MessageBox.Show("hadi yine iyisn ekledim seni ");
                //Getir();
            }
            crs.Close();
        }

        private void btnGüncelle_Click(object sender, EventArgs e)
        {

            crs.Open();
            SqlCommand baglanti = new SqlCommand("Update T_Musteri set Adi='" + txtadi.Text + "', Aciklama='" + txtaciklama.Text + "', miktar='" + txtmiktar.Text + "'  where UrunID=" + txturunno.Text + "", crs);
            int son = baglanti.ExecuteNonQuery();
            if (son > 0)
            {
                MessageBox.Show("Güncelleme Başarılı :) ");
            }
            crs.Close();
        }

        private void btnSil_Click(object sender, EventArgs e)
        {

            crs.Open();
            SqlCommand baglanti = new SqlCommand("delete from T_Musteri where URUNID=" + txturunno.Text + "", crs);
            int son = baglanti.ExecuteNonQuery();
            if (son > 0)
            {
                MessageBox.Show("sildim seni :) ");
            }
            crs.Close();
        }

        private void btnGec_Click(object sender, EventArgs e)
        {
            ürünform frm = new ürünform();
            frm.ShowDialog();
        }

        private void button4_Click(object sender, EventArgs e)
        {

            SqlDataAdapter da = new SqlDataAdapter("select * from T_URUN", crs);

            DataTable dt = new DataTable();
            da.Fill(dt);

            dataGridView1.DataSource = dt;
        }

        private void dataGridView1_CellMouseDoubleClick(object sender, DataGridViewCellMouseEventArgs e)
        {
            int sirano = dataGridView1.CurrentCell.RowIndex;
            txtadi.Text = dataGridView1.Rows[sirano].Cells["Adi"].Value.ToString();
            txtaciklama.Text = dataGridView1.Rows[sirano].Cells["Aciklama"].Value.ToString();
            txtmiktar.Text = dataGridView1.Rows[sirano].Cells["Miktar"].Value.ToString();
            txturunno.Text = dataGridView1.Rows[sirano].Cells["UrunID"].Value.ToString();

        }
    }
}
