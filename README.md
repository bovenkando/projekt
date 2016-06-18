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
        
        WebBrowser browser = new WebBrowser();
            int i = 0;

        private void Wstecz_Click(object sender, EventArgs e)
        {
            ((WebBrowser)tabControl1.SelectedTab.Controls[0]).Refresh();
        }

        private void Dalej_Click(object sender, EventArgs e)
        {
            ((WebBrowser)tabControl1.SelectedTab.Controls[0]).GoForward();
            
             using (System.IO.StreamWriter file = new System.IO.StreamWriter("historia.txt", true))
            {
                file.WriteLine(textBox1.Text);
            }
        }

        private void Odśwież_Click(object sender, EventArgs e)
        {
            okienko_na_strone.Refresh();
        }

        private void strona_startowa_Click(object sender, EventArgs e)
        {
             ((WebBrowser)tabControl1.SelectedTab.Controls[0]).Navigate("http://www.google.com");
        }

        private void Przejdź_Click(object sender, EventArgs e)
        {
            ((WebBrowser)tabControl1.SelectedTab.Controls[0]).Navigate(textBox1.Text);
            
            using (System.IO.StreamWriter file = new System.IO.StreamWriter("historia.txt", true))
            {
                file.WriteLine(textBox1.Text);
            }
        }

        private void Zatrzymaj_Click(object sender, EventArgs e)
        {
            ((WebBrowser)tabControl1.SelectedTab.Controls[0]).Stop();
        }
        private void nowakarta_Click(object sender, EventArgs e) 
        {
            browser = new WebBrowser();
            browser.ScriptErrorsSuppressed = true;
            browser.Dock = DockStyle.Fill;
            browser.Visible = true;
            browser.DocumentCompleted += browser_DocumentCompleted;
            browser.Navigate("http://www.google.com");
            tabControl1.Anchor = AnchorStyles.Top & AnchorStyles.Bottom & AnchorStyles.Right & AnchorStyles.Left;
            tabControl1.TabPages.Add("New tab");
            tabControl1.SelectTab(i);
            tabControl1.SelectedTab.Controls.Add(browser);
            i += 1;

        }
        private void usuńkartę_Click(object sender, EventArgs e)
        {
            if (tabControl1.TabPages.Count - 1 > 0) 
            {
                tabControl1.TabPages.RemoveAt(tabControl1.SelectedIndex);
                tabControl1.SelectTab(tabControl1.TabPages.Count - 1);
                i -= 1; 

            }
        }
        private void toolStripMenuItem1_Click(object sender, EventArgs e)
        {
            ColorDialog colorDLG = new ColorDialog();// funkcja umożliwiająca zmiane koloru tekstu
            if (colorDLG.ShowDialog() == System.Windows.Forms.DialogResult.OK) 
            {

                strona_startowa.ForeColor = colorDLG.Color;
                zatrzymaj.ForeColor = colorDLG.Color;
                wstecz.ForeColor = colorDLG.Color;
                dalej.ForeColor = colorDLG.Color;
                odśwież.ForeColor = colorDLG.Color;
                idź.ForeColor = colorDLG.Color;
                dodaj_kartę.ForeColor = colorDLG.Color;
                usuń_kartę.ForeColor = colorDLG.Color;
            }
        }
        private void kolorTłaToolStripMenuItem_Click(object sender, EventArgs e)
        {
            ColorDialog colorDLG = new ColorDialog();// funkcja umożliwiająca zmiane koloru tekstu
            if (colorDLG.ShowDialog() == System.Windows.Forms.DialogResult.OK)
            {
                this.BackColor = colorDLG.Color;
            }
        }

        private void textBox1_TextChanged(object sender, EventArgs e)
        {

        }
        private void Form1_Load(object sender, EventArgs e)
        {
            browser = new WebBrowser();
            browser.ScriptErrorsSuppressed = true;
            browser.Dock = DockStyle.Fill;
            browser.Visible = true;
            browser.DocumentCompleted += browser_DocumentCompleted;
            browser.Navigate("http://www.google.com");
            tabControl1.Anchor = AnchorStyles.Top & AnchorStyles.Bottom & AnchorStyles.Right & AnchorStyles.Left;
            tabControl1.TabPages.Add("New tab");
            tabControl1.SelectTab(i);
            tabControl1.SelectedTab.Controls.Add(browser);
            i += 1;

        }

       private void ądaneToolStripMenuItem_Click(object sender, EventArgs e ) // tworzenie histori
        {
            string[] lines = System.IO.File.ReadAllLines("historia.txt");//tworzenie tablicy z adresami do stron i zapis ich do pliku
            if (lines.Length < 5)
            {

                MessageBox.Show("Za malo stron by je wyswietlic", "Error");
            }

            else
            {
                MessageBox.Show(lines[lines.Length - 1] + "\n" + lines[lines.Length - 2] + "\n" + lines[lines.Length - 3] + "\n" + lines[lines.Length - 4] + "\n" + lines[lines.Length - 5] + "\n", "Historia");
            }
        }
         private void twórcyToolStripMenuItem_Click(object sender, EventArgs e)
        {
            MessageBox.Show("Wykonanie Katarzyna Skorupska & Wojciech Szczepek");// okienko pokazujące twórców
        }
        public void Update(Action action, string address)
        {
            WebBrowser wb = (WebBrowser)tabControl1.SelectedTab.Controls[0];
            switch (action)
            {
                case Action.NAVIGATE:
                    wb.Navigate(address);
                    break;
                case Action.GO_FORWARD:
                    wb.GoForward();
                    break;
                case Action.GO_BACK:
                    wb.GoBack();
                    break;
                case Action.REFRESH:
                    wb.Refresh();
                    break;
                case Action.STOP:
                    wb.Stop();
                    break;
            }
        }
        
        
    }
}
