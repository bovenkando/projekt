# projekt
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace projekt2
{
    public partial class Przegladarka : Form
    {
        public Przegladarka()
        {
            InitializeComponent();
        }

        private void Wstecz_Click(object sender, EventArgs e)
        {
            okienko_na_strone.GoBack();
        }

        private void Dalej_Click(object sender, EventArgs e)
        {
            okienko_na_strone.GoForward();
        }

        private void Odśwież_Click(object sender, EventArgs e)
        {
            okienko_na_strone.Refresh();
        }

        private void button4_Click(object sender, EventArgs e)
        {

        }

        private void button5_Click(object sender, EventArgs e)
        {

        }

        private void button6_Click(object sender, EventArgs e)
        {

        }

        private void textBox1_TextChanged(object sender, EventArgs e)
        {

        }

        private void webBrowser1_DocumentCompleted(object sender, WebBrowserDocumentCompletedEventArgs e)
        {

        }
    }
}
