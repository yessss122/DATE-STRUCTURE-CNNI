MatrixWhiz- Temă proiect "Date structure"
 Secțiunea "Educațional"
 NumeElev: Bobea Alin-Gabriel
 Profesor Coordonator: Petre Florin
 Școala: Colegiul Național "Nicolae Iorga", Vălenii de Munte
 SECȚIUNEA 1. Descrierea proiectului
 MatrixWhiz este o aplicație inovatoare și captivantă proiectată pentru a facilita învățarea și 
explorarea matricelor într-un mod interactiv și distractiv. Cu o interfață intuitivă și o gamă 
diversă de caracteristici, MatrixWhiz aduce lumea complexă a matricelor la îndemâna 
utilizatorilor de toate nivelele de experiență în programare și matematică.
 SECȚIUNEA 2. Principii și idei folosite la crearea acestui program
 Reflectând asupra programului, Bobea Alin-Gabriel a respectat toate principiile enunțate în 
regulamentul acestei competiții. Afirmăm că toate materialele sunt create de noi, cu mici 
excepții, anume:-Ecuațiile pentru fractal.-Această versiune de minesweeper este concepută și facută de noi, însă noi nu deținem 
jocul original.
 SECȚIUNEA 3. Conținutul programului
 SECȚIUNEA 3.1 Paginile principale/meniuri
 1. Pagina de login
 Acest cod gestionează autentificarea unui utilizator prin conectarea la o bază de date locală. 
Utilizatorul poate vizualiza sau ascunde parola bifând o casetă de selecție. La apăsarea 
butonului de autentificare, codul verifică emailul și parola în baza de date. Dacă datele sunt 
corecte, utilizatorul este autentificat și formularul principal se deschide. Dacă autentificarea 
eșuează, este afișat un mesaj de eroare. De asemenea, codul gestionează deschiderea și 
1
închiderea formularului de înregistrare printr-un link.
 publicpartialclasslogin: Form
 {
    SqlConnection con = newSqlConnection(@"Data 
Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename="+ 
Directory.GetParent(Directory.GetCurrentDirectory()).Parent.FullName + 
@"\Database1.mdf;Integrated Security=True");
    SqlCommand com;
    SqlDataReader dr;
    acasa form;
    Form9 register;
    boolregister_deschis = false;
    publicstaticstringutilizator_logat;
    publiclogin()
    {
        InitializeComponent();
    }
    private voidcheckBox1_CheckedChanged(objectsender, EventArgs e)
    {
        if(checkBox1.Checked)
        {
            textBox2.PasswordChar = '\0';
        }
        else
        {
            textBox2.PasswordChar = '*';
        }
    }
    private voidbutton1_Click(objectsender, EventArgs e)
 2
    {
        con.Open();
        com = newSqlCommand("select * from utilizatori where email = @e and 
parola = @p", con);
        com.Parameters.AddWithValue("@e", textBox1.Text);
        com.Parameters.AddWithValue("@p", textBox2.Text);
        dr = com.ExecuteReader();
        if(dr.HasRows)
        {
            while(dr.Read())
            {
                utilizator_logat = dr["prenume"].ToString();
                MessageBox.Show(utilizator_logat);
            }
            this.Hide();
            form = newacasa();
            form.Show();
        }
        else
        {
            label3.Visible = true;
            textBox1.Text = "";
            textBox2.Text = "";
        }
        con.Close();
    }
    private voidlinkLabel1_LinkClicked(objectsender, 
LinkLabelLinkClickedEventArgs e)
    {
 3
        if(!register_deschis)
        {
            register = newForm9();
            register.Show();
            register_deschis = true;
        }
        else
        {
            register_deschis = false;
            register.Close();
        }
    }
 }
 2. Pagina de register
 Acest cod gestionează înregistrarea unui utilizator în aplicație. Conectează aplicația la o 
bază de date locală pentru a verifica existența unui email introdus de utilizator. Dacă 
emailul există deja, afișează un mesaj de eroare. Dacă nu, înregistrează utilizatorul cu datele 
introduse și afișează un mesaj de confirmare. Codul permite, de asemenea, vizualizarea sau 
ascunderea caracterelor parolei în funcție de starea casetelor de selecție.
    publicpartialclassForm9: Form
    {
        SqlConnection con = newSqlConnection(@"Data 
Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename="+ 
Directory.GetParent(Directory.GetCurrentDirectory()).Parent.FullName + 
@"\Database1.mdf;Integrated Security=True");
        SqlCommand com;
        SqlDataReader dr;
        acasa form;
        publicstaticstringutilizator_logat;
        publicForm9()
        {
 4
            InitializeComponent();
        }
        privatevoidcheckBox1_CheckedChanged(objectsender, EventArgs e)
        {
            if(checkBox1.Checked)
            {
                textBox2.PasswordChar = '\0';
            }
            else
            {
                textBox2.PasswordChar = '*';
            }
        }
        privatevoidbutton1_Click(objectsender, EventArgs e)
        {
            com = newSqlCommand("select * from utilizatori where email=@t", 
con);
            com.Parameters.AddWithValue("@t", textBox1.Text);
            con.Open();
            dr = com.ExecuteReader();
            if(dr.HasRows)
            {
                dr.Close();
                label9.Visible = true;
            }
            else
            {
                dr.Close();
                com = newSqlCommand("insert into utilizatori (email, parola, 
nume, prenume) values (@email, @parola, @nume, @prenume)", con);
 5
                com.Parameters.AddWithValue("@email", textBox1.Text);
                com.Parameters.AddWithValue("@parola", textBox2.Text);
                com.Parameters.AddWithValue("@nume", textBox4.Text);
                com.Parameters.AddWithValue("@prenume", textBox5.Text);
                dr = com.ExecuteReader();
                MessageBox.Show("Cont inregistrat! Vă mulțumim!");
            }
            con.Close();
        }
        privatevoidcheckBox2_CheckedChanged(objectsender, EventArgs e)
        {
            if(checkBox2.Checked)
            {
                textBox3.PasswordChar = '\0';
            }
            else
            {
                textBox3.PasswordChar = '*';
            }
        }
    }
 3. Pagina de acasă
 Este meniul principal. De aici utilizatorul poate selecta mai multe meniuri pentru a le 
parcurge. Codul este simplu, toate butoanele folosesc un cod identic, singura 
diferență fiind numele variabilelor.
 publicpartialclassacasa: Form
 {
     intform_deschis = 0;
     intform_deschis1 = 0;
 6
     intform_deschis2 = 0;
     intform_deschis3 = 0;
     intform_deschis4 = 0;
     intform_deschis5 = 0;
     intcount = 0;
     boolpauza = false;
     informatii form2;
     meniu_aplicatii form5;
     meniu_chestionare form6;
     meniu_diverse form7;
     intr = 106;
     intg = 90;
     intb = 205;
     privateSize marime_formular;
     privateRectangle gradient;
     privateintopacitate = 255;
     Font font = newFont("Arial", 16);
     privateintform_x;
     privateintform_y;
     string[] v = new string[1];
     intk, i = 0, l;
     intlungsubsir = 0;
     privateStreamReader str;
     strings, s1;
     System.Windows.Forms.Timer timer;
     stringcitat;
     publicacasa()
     {
         InitializeComponent();
 7
         label6.Text = login.utilizator_logat;
         if(login.utilizator_logat == null)
         {
             label6.Text = "UTILIZATOR";
         }
         str = newStreamReader("citate.txt");
         timer1.Start();
         timer2.Interval = 40;
         timer3.Interval = 2000;
         CenterToScreen();
         marime_formular = this.Size;
         this.Paint += newPaintEventHandler(set_fundal);
     }
     privatevoidset_fundal(Object sender, PaintEventArgs e)
     {
         Graphics graphics = e.Graphics;
         gradient = newRectangle(0, 0, Width, Height);
         Brush a = newSolidBrush(Color.FromArgb(opacitate, 0, 0, 0));
         Brush b = newLinearGradientBrush(gradient, Color.FromArgb(57, 20, 127), 
Color.FromArgb(60, 120, 210), 65f);
         graphics.FillRectangle(b, gradient);
     }
     privatevoidbutton1_Click(objectsender, EventArgs e)
     {
         if(form_deschis == 0)
         {
             form2 = newinformatii();
             form2.Show();
             form_deschis = 1;
         }
 8
         else
         {
             form2.Close();
             form_deschis = 0;
         }
     }
     privatevoidasteapta(intmilliseconds)
     {
         Task.Delay(milliseconds);
     }
     privatevoidbutton2_Click(objectsender, EventArgs e)
     {
         if(form_deschis3 == 0)
         {
             form5 = newmeniu_aplicatii();
             form5.Show();
             form_deschis3 = 1;
         }
         else
         {
             form5.Close();
             form_deschis3 = 0;
         }
     }
     privatevoidbutton3_Click(objectsender, EventArgs e)
     {
         if(form_deschis4 == 0)
         {
             form6 = newmeniu_chestionare();
 9
             form6.Show();
             form_deschis4 = 1;
         }
         else
         {
             form6.Close();
             form_deschis4 = 0;
         }
     }
     privatevoidbutton4_Click(objectsender, EventArgs e)
     {
         if(form_deschis5 == 0)
         {
             form7 = newmeniu_diverse();
             form7.Show();
             form_deschis5 = 1;
         }
         else
         {
             form6.Close();
             form_deschis5 = 0;
         }
     }
     privatevoidtimer1_Tick(objectsender, EventArgs e)
     {
         if(str == null|| str.EndOfStream)
         {
             str = newStreamReader("citate.txt");
         }
 10
         citat = str.ReadLine();
         count = 0;
         timer2.Start();
         timer1.Stop();
     }
     privateasyncTask scrie_citat()
     {
         if(citat != null)
         {
             if(count < citat.Length)
             {
                 label3.Text += citat[count];
                 count++;
             }
             else
             {
                 awaitTask.Delay(4000);
                 label3.Text = "";
                 timer2.Stop();
                 timer1.Start();
             }
         }
         else
         {
             label3.Text = "NULL";                   
         }
     }
     privateasyncvoidtimer2_Tick(objectsender, EventArgs e)
     {
 11
         awaitscrie_citat();
     }
 }
 4. Meniul pentru informații
 Meniul cu informații generale despre proiect, folosește un 
gradient brush pentru a da un efect frumos fundalului.
 publicpartialclassinformatii: Form
 {
    informatii form2;
    privateRectangle gradient;
    private intopacitate = 255;
    Font font = newFont("Arial", 16);
    publicinformatii()
    {
        InitializeComponent();
        this.Paint += newPaintEventHandler(set_fundal);
    }
    private voidset_fundal(Object sender, PaintEventArgs e)
    {
        Graphics graphics = e.Graphics;
        gradient = newRectangle(0, 0, Width, Height);
        Brush a = newSolidBrush(Color.FromArgb(opacitate, 0, 0, 0));
        Brush b = newLinearGradientBrush(gradient, Color.FromArgb(57, 20, 127), 
Color.FromArgb(60, 120, 210), 65f);
        SizeF textSize = graphics.MeasureString("PROIECT (am uitat numele)", 
font);
        floatx = (Width -textSize.Width) / 2;
        floaty = (Height -textSize.Height) / 4 -textSize.Height / 2;
        PointF puncte = newPointF(x, y);
        graphics.FillRectangle(b, gradient);
 12
    }
 }
 5. Meniul pentru diverse
 Conține toate lecțiile/parcurgeriile. Are aproape același cod 
în butoane ca meniul de acasă, excepția fiind numele 
variabilelor.
 publicpartialclassmeniu_diverse: Form
 {
    item1 item1;
    item2 item2;
    item3 item3;
    item4 item4;
    item5 item5;
    item6 item6;
    item7 item7;
    item8 item8;
    item9 item9;
    item10 item10;
    item11 item11;
    item12 item12;
    item13 item13;
    item14 item14;
    item15 item15;
    item16 item16;
    item17 item17;
    item18 item18;
    publicboolformal = false;
    publicboolnon_formal = false;
    publicboolinformal = false;
    publicmeniu_diverse()
 13
    {
        InitializeComponent();
    }
    private voidbutton1_Click(objectsender, EventArgs e)
    {
        if(!formal)
        {
            panel1.Show();
            panel2.Hide();
            formal = true;
            informal = false;
        }
        else
        {
            panel1.Hide();
            formal = false;
            informal = false;
        }
    }
    private voidbutton2_Click(objectsender, EventArgs e)
    {
        item1 = newitem1();
        item1.Show();
    }
    private voidpanel1_Paint(objectsender, PaintEventArgs e)
    {
 14
    }
    private voidbutton5_Click(objectsender, EventArgs e)
    {
        item2 = newitem2();
        item2.Show();
    }
    private voidbutton8_Click(objectsender, EventArgs e)
    {
        item5 = newitem5();
        item5.Show();
    }
    private voidbutton6_Click(objectsender, EventArgs e)
    {
        item3 = newitem3();
        item3.Show();
    }
    private voidbutton9_Click(objectsender, EventArgs e)
    {
        item4 = newitem4();
        item4.Show();
    }
    private voidbutton7_Click(objectsender, EventArgs e)
    {
 15
        item13 = newitem13();
        item13.Show();
    }
    private voidbutton12_Click(objectsender, EventArgs e)
    {
        item14 = newitem14();
        item14.Show();
    }
    private voidbutton20_Click(objectsender, EventArgs e)
    {
        item6 = newitem6();
        item6.Show();
    }
    private voidbutton18_Click(objectsender, EventArgs e)
    {
        item7 = newitem7();
        item7.Show();
    }
    private voidbutton19_Click(objectsender, EventArgs e)
    {
        item12 = newitem12();
    }
    private voidbutton17_Click(objectsender, EventArgs e)
    {
 16
        item16 = newitem16();
        item16.Show();
    }
    private voidbutton16_Click(objectsender, EventArgs e)
    {
        item17 = newitem17();
        item17.Show();
    }
    private voidbutton15_Click(objectsender, EventArgs e)
    {
        item11 = newitem11();
        item11.Show();
    }
    private voidbutton14_Click(objectsender, EventArgs e)
    {
        item10 = newitem10();
        item10.Show();
    }
    private voidbutton13_Click(objectsender, EventArgs e)
    {
        item9 = newitem9();
        item9.Show();
    }
    private voidbutton3_Click(objectsender, EventArgs e)
 17
    {
        item8 = newitem8();
        item8.Show();
    }
    private voidbutton4_Click(objectsender, EventArgs e)
    {
        if(!informal)
        {
            panel1.Hide();
            panel2.Show();
            informal = true;
            formal = false;
        }
        else
        {
            panel2.Hide();
            informal = false;
            formal = false;
        }
    }
    private voidbutton10_Click(objectsender, EventArgs e)
    {
        item15 = newitem15();
        item15.Show();
    }
    private voidbutton11_Click(objectsender, EventArgs e)
 18
    {
        item18 = newitem18();
        item18.Show();
    }
 }
 6. Meniul pentru aplicații
 Conține jocurile, identic din punct de vedere tehnic ca meniul 
de diverse.
 publicpartialclassmeniu_aplicatii: Form
 {
    puzzle form6;
    meniu_minesweeper form7;
    quiz1 quiz1;
    x_0 form8;
    intform_deschis1 = 0;
    intform_deschis2 = 0;
    intform_deschis3 = 0;
    intform_deschis4 = 0;
    publicmeniu_aplicatii()
    {
        InitializeComponent();
    }
    private voidbutton1_Click(objectsender, EventArgs e)
    {
        if(form_deschis1 == 0)
        {
            form6 = newpuzzle();
            form6.Show();
 19
            form_deschis1 = 1;
        }
        else
        {
            form6.Close();
            form_deschis1 = 0;
        }
    }
    private voidbutton4_Click(objectsender, EventArgs e)
    {
        if(form_deschis2 == 0)
        {
            form7 = newmeniu_minesweeper();
            form7.Show();
            form_deschis2 = 1;
        }
        else
        {
            form7.Close();
            form_deschis2 = 0;
        }
    }
    private voidbutton2_Click(objectsender, EventArgs e)
    {
        if(form_deschis3 == 0)
        {
            form8 = newx_0();
 20
            form8.Show();
            form_deschis3 = 1;
        }
        else
        {
            form8.Close();
            form_deschis3 = 0;
        }
    }
    private voidbutton3_Click(objectsender, EventArgs e)
    {
        if(form_deschis3 == 0)
        {
            quiz1 = newquiz1();
            quiz1.Show();
            form_deschis4 = 1;
        }
        else
        {
            quiz1.Close();
            form_deschis4 = 0;
        }
    }
 }
 7. Meniul pentru chestionare
 Conține toate chestionarele. Identic din punct de vedere tehnic 
cu meniul de diverse.
 publicpartialclassmeniu_chestionare: Form
 21
{
    intform_deschis = 0;
    intform_deschis1 = 0;
    intform_deschis2 = 0;
    quiz1 q1;
    quiz2 q2;
    quiz3 q3;
    publicmeniu_chestionare()
    {
        InitializeComponent();
    }
    private voidbutton3_Click(objectsender, EventArgs e)
    {
        if(form_deschis == 0)
        {
            q1 = newquiz1();
            q1.Show();
            form_deschis = 1;
        }
        else
        {
            q1.Close();
            form_deschis = 0;
        }
    }
    private voidbutton6_Click(objectsender, EventArgs e)
    {
 22
        if(form_deschis1 == 0)
        {
            q2 = newquiz2();
            q2.Show();
            form_deschis1 = 1;
        }
        else
        {
            q2.Close();
            form_deschis1 = 0;
        }
    }
    private voidbutton5_Click(objectsender, EventArgs e)
    {
        if(form_deschis2 == 0)
        {
            q3 = newquiz3();
            q3.Show();
            form_deschis2 = 1;
        }
        else
        {
            q3.Close();
            form_deschis2 = 0;
        }
    }
 }
 SECȚIUNEA 3.2 Aplicații și diverse
 23
1. Parcurgerea unei matrici deasupra diagonalei principale
 Acest cod implementează o parcurgere a unei matrici deasupra diagonalei 
principale într-o aplicație de ferestre. La început, sunt definite variabilele și 
inițializate elementele grafice necesare. Apoi, în funcția parcurgere1_Shown, 
se construiește și se desenează matricea, iar apoi se inițiază o parcurgere a 
elementelor acesteia printr-un timer. La fiecare ticăit al timerului, un punct de 
deasupra diagonalei principale este colorat.
 publicpartialclassitem1: Form
 {
    intnr, nr1;
    Graphics g;
    Class1[] v = newClass1[1000];
    Rectangle[,] a = newRectangle[100, 100];
    SolidBrush s = newSolidBrush(Color.Red);
    item2 form;
    publicitem1()
    {
        InitializeComponent();
    }
    private voidbutton2_Click(objectsender, EventArgs e)
    {
            
    }
    private asyncvoidtimer1_Tick(objectsender, EventArgs e)
    {
        if(nr1 == nr)
        {
            timer1.Stop();
 24
        }
        else
        {
            nr1++;
            g.FillEllipse(s, a[v[nr1].x, v[nr1].y]);
        }
    }
    private voidparcurgere1_Shown(objectsender, EventArgs e)
    {
        g = this.CreateGraphics();
        Pen p = newPen(Color.Blue, 1);
        SolidBrush diag = newSolidBrush(Color.Blue);
        SolidBrush s = newSolidBrush(Color.Green); 
        for(inti = 1; i <= 6; i++)
            for(intj = 1; j <= 6; j++)
            {
                a[i, j] = newRectangle();
                a[i, j].Height = 50;
                a[i, j].Width = 50;
                a[i, j].Location = newPoint(5 + i * 56, 15 + j * 56);
                if(i == j)
                {
                    g.DrawEllipse(p, a[i, j]);
                    g.FillEllipse(diag, a[i, j]);
                }
                else
                {
 25
                    g.FillEllipse(s, a[i, j]);
                }
            }
        nr = 0;
        for(inti = 0; i < 6; i++)
        {
            for(intj = 0; j <= i; j++)
            {
                nr++;
                v[nr] = newClass1();
                v[nr].x = 6 -i + j;
                v[nr].y = j;
            }
            nr1 = 0;
            timer1.Start();
        }
    }
    private asyncTask afiseaza_urmatorul()
    {
        item2 nextForm = newitem2();
        nextForm.Show();
        awaitTask.Delay(100);
        this.Close();
    }
    private voidanimatie()
    {
        nr = 0;
 26
        for(inti = 0; i < 6; i++)
        {
            for(intj = 0; j < 6; j++)
            {
                if(i + j == 6 -1)
                {
                    nr++;
                    v[nr] = newClass1();
                    v[nr].x = i;
                    v[nr].y = j;
                }
            }
        }
        nr1 = 0;
        timer1.Start();
    }
    private voiditem1_Load(objectsender, EventArgs e)
    {
    }
    private voidincepe()
    {
        g = this.CreateGraphics();
        Pen p = newPen(Color.Blue, 1); 
        SolidBrush diag = newSolidBrush(Color.Blue);
        SolidBrush s = newSolidBrush(Color.Green); 
        for(inti = 1; i <= 6; i++)
 27
            for(intj = 1; j <= 6; j++)
            {
                a[i, j] = newRectangle();
                a[i, j].Height = 50;
                a[i, j].Width = 50;
                a[i, j].Location = newPoint(5 + i * 56, 15 + j * 56);
                if(i == j)
                {
                    g.DrawEllipse(p, a[i, j]);
                    g.FillEllipse(diag, a[i, j]);
                }
                else
                {
                    g.FillEllipse(s, a[i, j]);
                }
            }
        nr = 0;
        for(inti = 0; i < 6; i++)
        {
            for(intj = 0; j <= i; j++)
            {
                nr++;
                v[nr] = newClass1();
                v[nr].x = 6 -i + j;
                v[nr].y = j;
            }
            nr1 = 0;
 28
            timer1.Start();
        }
    }
 }
 2. Parcurgerea unei matrici deasupra diagonalei secundare
 Codul este aproape identic cu cel de mai sus, singura diferență fiind că cel de 
mai jos parcurge elementele unei matrici deasupra diagonalei secundare.
 publicpartialclassitem2: Form
 {
    intnr, nr1;
    Graphics g;
    Class1[] v = newClass1[1000];
    Rectangle[,] a = newRectangle[100, 100];
    SolidBrush s = newSolidBrush(Color.Red); 
    SolidBrush blue = newSolidBrush(Color.Blue);
    SolidBrush green = newSolidBrush(Color.Green);
    publicitem2()
    {
        InitializeComponent();
    }
    private voidbutton1_Click(objectsender, EventArgs e)
    {
            
    }
    private asyncvoidtimer1_Tick(objectsender, EventArgs e)
    {
        if(nr1 == nr)
        {
            timer1.Stop();
            if(!timer1.Enabled)
 29
            {
                awaitTask.Delay(1000);
                this.Close();
            }
        }
        else
        {
            nr1++;
            g.FillEllipse(s, a[v[nr1].x, v[nr1].y]);
        }
    }
    private voidparcurgere2_Load(objectsender, EventArgs e)
    {
    }
    private voidincepe()
    {
        g = this.CreateGraphics();
        Pen p = newPen(Color.Red, 1);
        Pen n = newPen(Color.Black, 1);
        for(inti = 1; i <= 6; i++)
        {
            for(intj = 1; j <= 6; j++)
            {
                a[i, j] = newRectangle();
                a[i, j].Height = 50;
                a[i, j].Width = 50;
                a[i, j].Location = newPoint(5 + i * 56, 15 + j * 56);
 30
                g.DrawEllipse(n, a[i, j]);
                if((i + j) == 7)
                {
                    g.FillEllipse(blue, a[i, j]);
                }
                if((i + j) > 7)
                {
                    g.FillEllipse(green, a[i, j]);
                }
            }
        }
    }
    private voidparcurgere2_Shown(objectsender, EventArgs e)
    {
        g = this.CreateGraphics();
        Pen p = newPen(Color.Red, 1);
        Pen n = newPen(Color.Black, 1);
        for(inti = 1; i <= 6; i++)
        {
            for(intj = 1; j <= 6; j++)
            {
                a[i, j] = newRectangle();
                a[i, j].Height = 50;
                a[i, j].Width = 50;
                a[i, j].Location = newPoint(5 + i * 56, 15 + j * 56);
                g.DrawEllipse(n, a[i, j]);
                if((i + j) == 7)
 31
                {
                    g.FillEllipse(blue, a[i, j]);
                }
                if((i + j) > 7)
                {
                    g.FillEllipse(green, a[i, j]);
                }
            }
        }
        nr = 0;
        for(inti = 0; i < 6; i++)
        {
            for(intj = 0; j <= i; j++)
            {
                nr++;
                v[nr] = newClass1();
                v[nr].x = i -j + 1;
                v[nr].y = j;
            }
            nr1 = 0;
            timer1.Start();
        }
    }
    private voidanimatie()
    {
        nr = 0;
        for(inti = 0; i < 6; i++)
        {
 32
            for(intj = 0; j <= i; j++)
            {
                nr++;
                v[nr] = newClass1();
                v[nr].x = i -j + 1;
                v[nr].y = j;
            }
            nr1 = 0;
            timer1.Start();
        }
    }
 }
 3. Parcurgerea unei matrici sub diagonala principală
 Codul este aproape identic cu cel de mai sus, singura diferență fiind că cel de 
mai jos parcurge elementele unei matrici sub diagonala principală.
 publicpartialclassitem3: Form
 {
    intnr, nr1;
    Graphics g;
    Class1[] v = newClass1[1000];
    Rectangle[,] a = newRectangle[100, 100];
    SolidBrush s = newSolidBrush(Color.Red);
    SolidBrush blue = newSolidBrush(Color.Blue);
    SolidBrush green = newSolidBrush(Color.Green);
    publicitem3()
    {
        InitializeComponent();
    }
    private voidanimatie()
    {
 33
        g = this.CreateGraphics();
        Pen p = newPen(Color.Red, 1);
        Pen n = newPen(Color.Black, 1);
        for(inti = 1; i <= 6; i++)
            for(intj = 1; j <= 6; j++)
            {
                a[i, j] = newRectangle();
                a[i, j].Height = 50;
                a[i, j].Width = 50;
                a[i, j].Location = newPoint(5 + i * 56, 15 + j * 56); //5 + i * 
56, 15 + j * 56
                g.DrawEllipse(n, a[i, j]);
                if(i == j)
                {
                    g.FillEllipse(blue, a[i, j]);
                }
                if((i -j) > 0)
                {
                    g.FillEllipse(green, a[i, j]);
                }
            }
        nr = 0;
        for(inti = 0; i < 6; i++)
        {
            for(intj = 0; j <= i; j++)
            {
                nr++;
                v[nr] = newClass1();
                v[nr].x = j;
 34
                v[nr].y = 6 -i + j;
            }
            nr1 = 0;
            timer1.Start();
        }
    }
    private voidparcurgere3_Shown(objectsender, EventArgs e)
    {
        animatie();
    }
    private asyncvoidtimer1_Tick(objectsender, EventArgs e)
    {
        if(nr1 == nr)
        {
            timer1.Stop();
            if(!timer1.Enabled)
            {
                awaitTask.Delay(1000);
                this.Close();
            }
        }
        else
        {
            nr1++;
            g.FillEllipse(s, a[v[nr1].x, v[nr1].y]);
        }
    }
 }
 4. Parcurgerea unei matrici sub diagonala secundară
 35
Codul este aproape identic cu cel de mai sus, singura diferență fiind că cel de 
mai jos parcurge elementele unei matrici sub diagonala secundară.
 publicpartialclassitem4: Form
 {
    intnr, nr1;
    Graphics g;
    Class1[] v = newClass1[1000];
    Rectangle[,] a = newRectangle[100, 100];
    SolidBrush s = newSolidBrush(Color.Red);
    SolidBrush blue = newSolidBrush(Color.Blue);
    SolidBrush green = newSolidBrush(Color.Green);
    publicitem4()
    {
        InitializeComponent();
    }
    private asyncvoidtimer1_Tick(objectsender, EventArgs e)
    {
        if(nr1 == nr) timer1.Stop();
        else
        {
            nr1++;
            g.FillEllipse(s, a[v[nr1].x, v[nr1].y]);
        }
    }
    private voidparcurgere4_Shown(objectsender, EventArgs e)
 36
    {
        animatie();
    }
    private voiditem4_Load(objectsender, EventArgs e)
    {
    }
    private voidanimatie()
    {
        g = this.CreateGraphics();
        Pen p = newPen(Color.Red, 1);
        Pen n = newPen(Color.Black, 1);
        for(inti = 1; i <= 6; i++)
            for(intj = 1; j <= 6; j++)
            {
                a[i, j] = newRectangle();
                a[i, j].Height = 50;
                a[i, j].Width = 50;
                a[i, j].Location = newPoint(5 + i * 56, 15 + j * 56); //5 + i * 
56, 15 + j * 56
                g.DrawEllipse(n, a[i, j]);
                if((i + j) == 7)
                {
                    g.FillEllipse(blue, a[i, j]);
                }
                if((i + j) < 7)
                {
 37
                    g.FillEllipse(green, a[i, j]);
                }
            }
        nr = 0;
        for(inti = 0; i < 5; i++)
        {
            for(intj = 0; j <= i; j++)
            {
                nr++;
                v[nr] = newClass1();
                v[nr].x = 6 -j;
                v[nr].y = 6 -i + j;
            }
            nr1 = 0;
            timer1.Start();
        }
    }
 }
 5. Matrice pliabilă din colț
 Acest cod definește o fereastră într-o aplicație care afișează o matrice care "se 
pliază" din colț. La început, sunt create și inițializate obiectele PictureBox 
pentru fiecare element din matrice. Aceste obiecte sunt adăugate pe fereastra 
curentă și inițial au dimensiuni zero și sunt colorate în roșu. Apoi, este pornit 
un timer care crește dimensiunile elementelor matricei astfel încât acestea să 
pară că "se pliază" din colț. După o anumită perioadă de timp, timerul se 
oprește și este pornit un alt timer care micșorează dimensiunile elementelor 
matricei, simulând "dezplierea" lor. Acest proces se repetă până când matricea 
este complet "dezpliată".
 publicpartialclassitem5: Form
 {
 38
    PictureBox[,] a = newPictureBox[100, 100];
    intk;
    publicitem5()
    {
        InitializeComponent();
    }
    private voiditem5_Shown(objectsender, EventArgs e)
    {
        for(inti = 0; i < 10; i++)
            for(intj = 0; j < 10; j++)
            {
                a[i, j] = newPictureBox();
                a[i, j].Height = 0;
                a[i, j].Width = 0;
                a[i, j].Location = newPoint(5 + i * 56, 15 + j * 32);
                a[i, j].BackColor = Color.Red;
                this.Controls.Add(a[i, j]);
            }
        k = 0;
        timer1.Start();
    }
    private asyncvoidtimer1_Tick(objectsender, EventArgs e)
    {
        if(k == 30)
        {
            timer1.Stop();
            awaitTask.Delay(1000);
 39
            k = 0;
            timer2.Start();
        }
        else
        {
            k++;
            for(inti = 0; i < 10; i++)
                for(intj = 0; j < 10; j++)
                {
                    a[i, j].Width += 1;
                    a[i, j].Height += 1;
                }
        }
    }
    private voidtimer2_Tick(objectsender, EventArgs e)
    {
        if(k == 30)
        {
            this.Close();
            timer2.Stop();
        }
        else
        {
            k++;
            for(inti = 0; i < 10; i++)
                for(intj = 0; j < 10; j++)
                {
                    a[i, j].Width -= 1;
 40
                    a[i, j].Height -= 1;
                }
        }
    }
    private voidlabel4_Click(objectsender, EventArgs e)
    {
    }
 }
 6. Animație de matrice în stil de ploaie
 La inițializare, se stabilesc parametrii de bază, cum ar fi 
dimensiunile celulelor și numărul de rânduri și coloane ale 
matricei care va reprezenta ploaia. Se utilizează o matrice de 
booleane pentru a indica dacă picăturile de ploaie sunt 
prezente sau nu în fiecare celulă.
 În funcția incepe_ploaia(), se stabilește inițializarea 
picăturilor de ploaie pe primul rând, iar în funcția picura(), 
picăturile sunt deplasate în jos și sunt simulate prin 
schimbarea stării lor în matricea de picături. Astfel, 
picăturile de ploaie sunt create în mod aleatoriu și călătoresc 
în jos până când ajung la partea de jos a ferestrei, moment în 
care dispar și pot fi create altele noi. Această simulare a 
ploii este actualizată și desenată în mod repetat la fiecare 
intervale regulate de timp folosind un timer.
 publicpartialclassitem6: Form
 {
    private constintCellSize = 10;
    private constintRows = 20;
    private constintColumns = 40;
    private bool[,] rainDrops = newbool[Rows, Columns];
    privateRandom random = newRandom();
 41
    privateTimer timer = newTimer();
    privateBrush brush = Brushes.Blue;
    publicitem6()
    {
        InitializeComponent();
        incepe_ploaia();
        timer1.Interval = 50;
        timer1.Start();
    }
    private voidtimer1_Tick(objectsender, EventArgs e)
    {
        picura();
        Invalidate();
    }
    private voidincepe_ploaia()
    {
        for(intj = 0; j < Columns; j++)
        {
            rainDrops[0, j] = random.Next(0, 10) == 0;
        }
    }
    private voidpicura()
    {
        for(inti = Rows -1; i >= 0; i--)
        {
            for(intj = 0; j < Columns; j++)
            {
 42
                if(rainDrops[i, j])
                {
                    rainDrops[i, j] = false;
                    if(i < Rows - 1)
                    {
                        rainDrops[i + 1, j] = true;
                    }
                }
            }
        }
        for(intj = 0; j < Columns; j++)
        {
            rainDrops[0, j] = random.Next(0, 10) == 0;
        }
    }
    protectedoverride voidOnPaint(PaintEventArgs e)
    {
        base.OnPaint(e);
        for(inti = 0; i < Rows; i++)
        {
            for(intj = 0; j < Columns; j++)
            {
                if(rainDrops[i, j])
                {
                    e.Graphics.FillRectangle(brush, j * CellSize, i * CellSize, 
CellSize, CellSize);
                }
            }
        }
 43
    }
 }
 7. Animație de matrice în stil de scântei
 Acest cod creează o animație de scântei care se deplasează în 
sus pe ecran. Sunt create 100 de scântei, fiecare cu o poziție 
și o dimensiune aleatorii. Acestea sunt reprezentate sub formă 
de elipse colorate cu o nuanță de galben către roșu, utilizând 
un gradient linear. La fiecare cadru de animație, scânteile se 
mișcă în sus cu o viteză aleatoare. Când o scânteie ajunge la 
partea de sus a ecranului, își resetează poziția și dimensiunea 
pentru a începe din nou.
 publicpartialclassitem7: Form
 {
    private readonlyRandom aleator = newRandom();
    private constintNumarScantei = 100;
    private readonlyScanteie[] scantei = newScanteie[NumarScantei];
    private readonlyBrush[] pensule = { Brushes.Yellow, Brushes.Orange, 
Brushes.Red };
    private constintDimensiuneScanteieMin = 3;
    private constintDimensiuneScanteieMax = 12;
    publicitem7()
    {
        InitializeComponent();
        InitializareScantei();
        StartArderi();
    }
    private voidtimer1_Tick(objectsender, EventArgs e)
    {
            
    }
 44
    private voidInitializareScantei()
    {
        for(inti = 0; i < NumarScantei; i++)
        {
            scantei[i] = newScanteie
            {
                X = aleator.Next(ClientSize.Width / 2 + 80),
                Y = aleator.Next(ClientSize.Height),
                Dimensiune = aleator.Next(DimensiuneScanteieMin, 
DimensiuneScanteieMax + 1)
            };
        }
    }
    private asyncvoidStartArderi()
    {
        while(true)
        {
            awaitTask.Delay(25); 
            for(inti = 0; i < NumarScantei; i++)
            {
                scantei[i].Y -= aleator.Next(1, 4); 
                if(scantei[i].Y < 0)
                {
                    scantei[i].Y = ClientSize.Height;
                    scantei[i].X = aleator.Next(ClientSize.Width / 2 + 80);
                    scantei[i].Dimensiune = aleator.Next(DimensiuneScanteieMin, 
DimensiuneScanteieMax + 1);
                }
 45
            }
            Invalidate(); 
        }
    }
    protectedoverride voidOnPaint(PaintEventArgs e)
    {
        foreach(var scanteie inscantei)
        {
            using(vargradienta = newLinearGradientBrush(newPoint(0, 
scanteie.Y), newPoint(0, scanteie.Y + scanteie.Dimensiune), Color.Yellow, 
Color.Red))
            {
                e.Graphics.FillEllipse(gradienta, scanteie.X, scanteie.Y, 
scanteie.Dimensiune, scanteie.Dimensiune);
            }
        }
    }
    private classScanteie
    {
        publicintX { get; set; }
        publicintY { get; set; }
        publicintDimensiune { get; set; }
    }
    private voiditem7_Paint(objectsender, PaintEventArgs e)
    {
           
46
    }
 }
 8. Simularea unor "licurici" folosind o matrice
 La inițializare, sunt stabilite dimensiunile matricei și 
numărul de particule de licurici care vor fi simulate. 
Particulele sunt plasate inițial în mod aleatoriu în matrice.
 Funcția timer1_Tick este responsabilă pentru actualizarea 
pozițiilor particulelor la fiecare interval de timp. Aceasta 
este realizată prin apelul funcției MoveParticles, care 
determină noile poziții ale particulelor conform unor reguli de 
mișcare aleatorii. Particulele se deplasează în toate 
direcțiile înconjurătoare în mod aleatoriu.
 În funcția OnPaint, matricea este desenată pe fereastra cu 
licurici, iar particulele sunt reprezentate prin dreptunghiuri 
albe pe fundalul negru, indicând prezența lor în matricea 
bidimensională.
 publicpartialclassitem9: Form
 {
    private constintWidth = 50;
    private constintHeight = 50;
    private constintNumParticles = 50;
    private bool[,] matrix = newbool[Width, Height];
    privateRandom rand = newRandom();
    publicitem9()
    {
        InitializeComponent();
        InitializeParticles();
        timer1.Interval = 50;
 47
        timer1.Start();
    }
    private voidInitializeParticles()
    {
        for(inti = 0; i < NumParticles; i++)
        {
            intx = rand.Next(Width);
            inty = rand.Next(Height);
            matrix[x, y] = true;
        }
    }
    private voidtimer1_Tick(objectsender, EventArgs e)
    {
        MoveParticles();
        Invalidate();
    }
    private voidMoveParticles()
    {
        bool[,] newMatrix = newbool[Width, Height];
        for(intx = 0; x < Width; x++)
        {
            for(inty = 0; y < Height; y++)
            {
                if(matrix[x, y])
                {
                    matrix[x, y] = false;
                    intnewX = (x + rand.Next(-1, 2) + Width) % Width;
                    intnewY = (y + rand.Next(-1, 2) + Height) % Height;
                    newMatrix[newX, newY] = true;
 48
                }
            }
        }
        matrix = newMatrix;
    }
    protectedoverride voidOnPaint(PaintEventArgs e)
    {
        base.OnPaint(e);
        Graphics g = e.Graphics;
        g.Clear(Color.Black);
        floatcellWidth = (float)ClientSize.Width / 2 / Width;
        floatcellHeight = (float)ClientSize.Height / Height;
        for(intx = 0; x < Width; x++)
        {
            for(inty = 0; y < Height; y++)
            {
                if(matrix[x, y])
                {
                    RectangleF rect = newRectangleF(x * cellWidth, y * 
cellHeight, cellWidth, cellHeight);
                    g.FillRectangle(Brushes.White, rect);
                }
            }
        }
    }
    private voidlabel4_Click(objectsender, EventArgs e)
    {
    }
 49
}
 9. Simulare expansiune 
La inițializare, zona este inițializată cu un anumit procentaj 
de celule aprinse, iar la fiecare ticăit al timerului, focul se 
extinde în zonele vecine ale celulelor deja aprinse. Noua 
poziție a focului este determinată aleatoriu între pozițiile 
disponibile din jurul unei celule aprinse.
 În funcția OnPaint, zona este desenată pe fereastră, iar 
celulele aprinse sunt reprezentate printr-un dreptunghi 
portocaliu.
 publicpartialclassitem10: Form
 {
    private constintWidth = 50;
    private constintHeight = 25;
    private constintmarime_celula = 10;
    private constdoubleprobabilitate = 0.15;
    private bool[,] grid = newbool[Width, Height];
    privateRandom random = newRandom();
    publicitem10()
    {
        InitializeComponent();
        fa_panou();
        timer1.Start();
    }
    private voiditem10_Load(objectsender, EventArgs e)
    {
    }
    private voidtimer1_Tick(objectsender, EventArgs e)
 50
    {
        extinde_foc();
        Invalidate();
    }
    private voidfa_panou()
    {
        for(intx = 0; x < Width; x++)
        {
            for(inty = 0; y < Height; y++)
            {
                grid[x, y] = random.NextDouble() < probabilitate;
            }
        }
    }
    private voidextinde_foc()
    {
        bool[,] newGrid = newbool[Width, Height];
        for(intx = 0; x < Width; x++)
        {
            for(inty = 0; y < Height; y++)
            {
                if(grid[x, y])
                {
                    newGrid[x, y] = true;
                    extinde(newGrid, x, y);
                }
                else
                {
 51
                    newGrid[x, y] = grid[x, y];
                }
            }
        }
        grid = newGrid;
    }
    private voidextinde(bool[,] panou_nou, intx, inty)
    {
        for(intdx = -1; dx <= 1; dx++)
        {
            for(intdy = -1; dy <= 1; dy++)
            {
                if((dx != 0 || dy != 0) && e_panou(x + dx, y + dy) && !grid[x + 
dx, y + dy])
                {
                    if(random.NextDouble() < 0.5) 
                    {
                        panou_nou[x + dx, y + dy] = true;
                    }
                }
            }
        }
    }
    private boole_panou(intx, inty)
    {
        returnx >= 0 && x < Width && y >= 0 && y < Height;
    }
    protectedoverride voidOnPaint(PaintEventArgs e)
    {
 52
        base.OnPaint(e);
        Graphics g = e.Graphics;
        g.Clear(Color.Black);
        for(intx = 0; x < Width; x++)
        {
            for(inty = 0; y < Height; y++)
            {
                if(grid[x, y])
                {
                    Rectangle rect = newRectangle(x * marime_celula, y * 
marime_celula, marime_celula, marime_celula);
                    g.FillRectangle(Brushes.OrangeRed, rect); 
                }
            }
        }
    }
 }
 10. Steluțe de gheață
 La inițializare, sunt create și desenate steluțe de gheață, 
fiecare formată din linii care se întâlnesc în centrul unui 
cerc imaginar.
 În funcția item11_Shown, sunt create și desenate steluțele de 
gheață în locațiile specificate. Desenarea este realizată prin 
intermediul funcției desen, care primește coordonatele de start 
ale steluței, dimensiunea acesteia și realizează desenarea 
efectivă.
 publicpartialclassitem11: Form
 {
    Rectangle[,] a = newRectangle[100, 100];
    Class1[] v = newClass1[1000];
 53
    intnr = 0, nr1;
    Graphics g;
    SolidBrush s = newSolidBrush(Color.Red);
    publicitem11()
    {
        InitializeComponent();
    }
    private voiditem11_Shown(objectsender, EventArgs e)
    {
        g = this.CreateGraphics();
        Pen p = newPen(Color.Red, 1);
        for(inti = 0; i < 6; i++)
            for(intj = 0; j < 6; j++)
            {
                a[i, j] = newRectangle();
                a[i, j].Height = 50;
                a[i, j].Width = 50;
                a[i, j].Location = newPoint(5 + i * 56, 15 + j * 56);
                desen(5 + i * 56, 15 + j * 56, 50);
            }
        for(inti = 0; i < 6; i++)
            for(intj = 0; j < 6; j++)
            {
                if(i > j)
                {
                    v[nr] = newClass1();
 54
                    v[nr].x = i;
                    v[nr].y = j; nr++;
                }
            }
        nr1 = 0;
        timer1.Start();
    }
    voiddesen(intx, inty, intd)
    {
        Graphics g = this.CreateGraphics();
        Pen blackPen = newPen(Color.Black, 1);
        Point start = newPoint(0, 0);
        Point end = newPoint(0, d / 2);
        g.TranslateTransform(x + d / 2, y + d / 2);
        for(inti = 1; i <= 12; i++)
        {
            g.DrawLine(blackPen, start, end);
            g.RotateTransform(30.0F);
        }
    }
    private voidtimer1_Tick(objectsender, EventArgs e)
    {
        if(nr1 == nr)
        {
            timer1.Stop();
        }
        else
 55
        {
            nr1++;
        }
    }
    private voiditem11_Load(objectsender, EventArgs e)
    {
    }
 }
 11. Fractal Mandelbrot
 Acest fractal este generat prin iterarea unui set de ecuații și 
colorarea pixelilor în funcție de numărul de iterații necesare 
pentru ca valoarea să depășească un anumit prag.
 În cadrul funcției item12_Shown, se definește dimensiunea 
imaginii fractalei și se creează o imagine goală. Apoi, pentru 
fiecare pixel din imagine, se calculează coordonatele 
corespunzătoare în planul complex și se aplică formula 
specifică fractalului Mandelbrot pentru a determina culoarea 
pixelului.
 Culoarea pixelilor este determinată în funcție de numărul de 
iterații necesare pentru a depăși un anumit prag. Dacă numărul 
de iterații depășește pragul maxim, pixelul este colorat în 
negru; altfel, culoarea este determinată în funcție de numărul 
de iterații și este atribuită pixelului în funcție de acesta.
 După ce toți pixelii sunt colorați, imaginea fractală este 
afișată într-un control PictureBox.
 publicpartialclassitem12: Form
 {
    publicitem12()
    {
 56
        InitializeComponent();
    }
    private voiditem12_Load(objectsender, EventArgs e)
    {
    }
    private voiditem12_Shown(objectsender, EventArgs e)
    {
        intwidth = 800;
        intheight = 600;
        Bitmap fractalImage = newBitmap(width, height);
        doublexMin = -2.5;
        doublexMax = 1.0;
        doubleyMin = -1.0;
        doubleyMax = 1.0;
        for(intxPixel = 0; xPixel < width; xPixel++)
        {
            for(intyPixel = 0; yPixel < height; yPixel++)
            {
                doublex0 = xMin + (xMax -xMin) * xPixel / (double)width;
                doubley0 = yMin + (yMax -yMin) * yPixel / (double)height;
                doublex = 0, y = 0;
                intiterations = 0;
 57
                intmaxIterations = 1000; 
                while(x * x + y * y <= 5 && iterations < maxIterations)
                {
                    doublexTemp = x * x -y * y + x0;
                    y = 2 * x * y + y0;
                    x = xTemp;
                    iterations++;
                }
                Color color;
                if(iterations == maxIterations)
                {
                    color = Color.Black; 
                }
                else
                {
                    intcolorValue = iterations % 256;
                    color = Color.FromArgb(colorValue, colorValue, colorValue);
                }
                fractalImage.SetPixel(xPixel, yPixel, color);
            }
            pictureBox1.Image = fractalImage;
        }
    }
 }
 12. Matrice pliantă orizontal
 La inițializare, sunt create controale PictureBox cu lățimea 
zero și înălțimea specificată, apoi acestea sunt adăugate pe 
58
fereastră. Un timer este pornit pentru a gestiona extinderea 
matricei de controale PictureBox în mod progresiv în timp.
 În funcția item13_Shown, sunt create controale PictureBox și 
sunt plasate pe fereastră într-o matrice de dimensiune 10x10, 
fiecare control având o înălțime fixă și o lățime inițială de 
zero. Aceste controale sunt colorate în roșu și sunt adăugate 
pe fereastră.
 Apoi, în funcția timer1_Tick, lățimea controalelor PictureBox 
este crescută treptat la fiecare ticăit al timerului, până când 
atinge valoarea de 40. La acest punct, timerul se oprește.
 publicpartialclassitem13: Form
 {
     PictureBox[,] a = newPictureBox[100, 100];
     intk;
     publicitem13()
     {
         InitializeComponent();
         timer1.Interval = 50;
     }
     privatevoiditem13_Shown(objectsender, EventArgs e)
     {
         for(inti = 0; i < 10; i++)
             for(intj = 0; j < 10; j++)
             {
                 a[i, j] = newPictureBox();
                 a[i, j].Height = 40;
                 a[i, j].Width = 0;
                 a[i, j].Location = newPoint(5 + i * 56, 15 + j * 56);
                 a[i, j].BackColor = Color.Red;
                 this.Controls.Add(a[i, j]);
 59
             }
         k = 0;
         timer1.Start();
     }
     privatevoidtimer1_Tick(objectsender, EventArgs e)
     {
         if(k == 40) timer1.Stop();
         else
         {
             k++;
             for(inti = 0; i < 10; i++)
                 for(intj = 0; j < 10; j++)
                     a[i, j].Width += 1;
         }
     }
 }
 13. Matrice pliantă vertical
 La inițializare, sunt create controale PictureBox cu înălțimea 
zero și lățimea specificată, apoi acestea sunt adăugate pe 
fereastră. Un timer este pornit pentru a gestiona extinderea 
matricei de controale PictureBox în mod progresiv în timp.
 În funcția item14_Shown, sunt create controale PictureBox și 
sunt plasate pe fereastră într-o matrice de dimensiune 10x10, 
fiecare control având o lățime fixă și o înălțime inițială de 
zero. Aceste controale sunt colorate în roșu și sunt adăugate 
pe fereastră.
 Apoi, în funcția timer1_Tick, înălțimea controalelor PictureBox 
este crescută treptat la fiecare ticăit al timerului, până când 
atinge valoarea de 30. La acest punct, timerul se oprește.
 60
publicpartialclassitem14: Form
 {
    PictureBox[,] a = newPictureBox[100, 100];
    intk;
    publicitem14()
    {
        InitializeComponent();
    }
    private voiditem14_Shown(objectsender, EventArgs e)
    {
        for(inti = 0; i < 10; i++)
            for(intj = 0; j < 10; j++)
            {
                a[i, j] = newPictureBox();
                a[i, j].Height = 0;
                a[i, j].Width = 30;
                a[i, j].Location = newPoint(5 + i * 56, 15 + j * 56);
                a[i, j].BackColor = Color.Red;
                this.Controls.Add(a[i, j]);
            }
        k = 0;
        timer1.Start();
    }
    private voidtimer1_Tick(objectsender, EventArgs e)
    {
        if(k == 30) timer1.Stop();
        else
        {
 61
            k++;
            for(inti = 0; i < 10; i++)
                for(intj = 0; j < 10; j++)
                    a[i, j].Height += 1;
        }
    }
 }
 14. Simulare program C#
 În cadrul acestei simulări, se utilizează un fișier text pentru 
a citi și afișa linii de cod, iar apoi se simulează execuția 
acestor linii de cod prin schimbarea culorii textului din 
albastru în roșu, pe măsură ce programul "rulează".
 În funcția item15_Shown, se încarcă și se afișează conținutul 
unui fișier text care conține liniile de cod ale programului de 
simulat. Fiecare linie este afișată printr-un control Label pe 
fereastră.
 Funcția suma_matrice simulează execuția programului C#. Acesta 
construiește o matrice, calculează suma elementelor pare și 
înregistrează secvența de execuție într-un vector de 
instrucțiuni.
 Funcția restart este apelată la fiecare trecere prin ciclul de 
execuție și reinițializează culorile textului la albastru 
pentru a indica că linia de cod respectivă nu este în execuție.
 Timerul timer1 este folosit pentru a simula execuția 
programului, prin trecerea prin secvența de instrucțiuni și 
schimbarea culorii textului corespunzător fiecărei linii de 
cod.
 publicpartialclassitem15: Form
 {
    inti = 0, nr = 0, m, it = -1;
    Label[] l = newLabel[100];
    int[] v = newint[100];
    publicitem15()
 62
    {
        InitializeComponent();
    }
    private voidtimer1_Tick(objectsender, EventArgs e)
    {
        if(it == nr -1) timer1.Stop();
        else
        {
            it++;
            restart();
            l[v[it % nr]].ForeColor = System.Drawing.Color.Red;
        }
    }
    private voiditem15_Shown(objectsender, EventArgs e)
    {
        using(StreamReader fin = newStreamReader("parcurgeri_matrici
 \\matrice.txt"))
        {
            while(!fin.EndOfStream)
            {
                strings = fin.ReadLine();
                l[i] = newLabel();
                l[i].Location = newPoint(100, 30 + i * 30);
                l[i].Size = newSize(350, 30);
                l[i].Font = newFont("Times New Roman", 16);
                l[i].Text = s;
                this.Controls.Add(l[i]);
                i++;
 63
            }
            fin.Close();
            m = i;
        }
        suma_matrice();
        timer1.Start();
        i = 0;
    }
    voidsuma_matrice()
    {
        intx;
        int[,] a = new int[100, 100]; x = 2; v[nr] = x; nr++;
        intn = 3, i, j, s = 0; x = 3; v[nr] = x; nr++;
        for(i = 1; i <= n; i++)
        {
            x = 4; v[nr] = x; nr++;
            for(j = 1; j <= n; j++)
            {
                x = 5; v[nr] = x; nr++;
                { a[i, j] = i + j; x = 6; v[nr] = x; nr++; }
            }
        }
        for(i = 1; i <= n; i++)
        {
            x = 7; v[nr] = x; nr++;
            for(j = 1; j <= n; j++)
            {
                x = 8; v[nr] = x; nr++;
 64
                if(a[i, j] % 2 == 0)
                {
                    x = 9; v[nr] = x; nr++;
                    s = s + a[i, j]; x = 10; v[nr] = x; nr++;
                }
            }
        }
    }
    voidrestart()
    {
        for(inti = 0; i < m; i++)
        {
            l[i].ForeColor = System.Drawing.Color.Blue;
        }
    }
 }
 15. Simularea răspândirii apei in vas
 Acest cod utilizează o rețea de butoane pentru a reprezenta 
starea apei în diferite celule ale vasului și un timer pentru a 
actualiza și desena starea apei în mod continuu.
 În funcția InitializeWaterGrid, se creează o rețea de butoane, 
fiecare reprezentând o celulă a vasului, și se inițializează 
nivelurile de apă pentru fiecare celulă cu valori aleatoare.
 Funcția item16_Shown pornește timerul pentru a începe 
simularea.
 Timerul timer1 declanșează actualizarea și desenarea stării 
apei la fiecare interval de timp specificat în Interval.
 Funcția UpdateWater calculează nivelurile de apă pentru fiecare 
celulă a vasului, luând în considerare și apa din celulele 
adiacente.
 65
Funcția DrawWater colorează butoanele reprezentând celulele 
vasului în funcție de nivelurile lor de apă, astfel încât 
culoarea să varieze de la albastru (nivel scăzut de apă) la alb 
(nivel înalt de apă).        privateconstintmarime_panou = 20;
        privateButton[,] panou_apa = newButton[marime_panou, marime_panou];
        privatefloat[,] nivel_apa = newfloat[marime_panou, marime_panou];
        privateRandom rand = newRandom();
        privateTimer timer = newTimer();
        publicitem16()
        {
            InitializeComponent();
            timer1.Interval = 250;
            InitializeWaterGrid();
        }
        privatevoidInitializeWaterGrid()
        {
            for(inti = 0; i < marime_panou; i++)
            {
                for(intj = 0; j < marime_panou; j++)
                {
                    Button button = newButton
                    {
                        Size = newSize(30, 30),
                        Location = newPoint(i * 30, j * 30),
                        BackColor = Color.Blue,
                        FlatStyle = FlatStyle.Flat
                    };
                    panou_apa[i, j] = button;
                    Controls.Add(button);
                }
 66
            }
            for(inti = 0; i < marime_panou; i++)
            {
                for(intj = 0; j < marime_panou; j++)
                {
                    nivel_apa[i, j] = (float)rand.NextDouble();
                }
            }
        }
        privatevoiditem16_Shown(objectsender, EventArgs e)
        {
            timer1.Start();
        }
        privatevoidtimer1_Tick(objectsender, EventArgs e)
        {
            UpdateWater();
            DrawWater();
        }
        privatevoidUpdateWater()
        {
            float[,] nivel_apa_urm = newfloat[marime_panou, marime_panou];
            for(inti = 0; i < marime_panou; i++)
            {
                for(intj = 0; j < marime_panou; j++)
                {
                    floatapa_totala = nivel_apa[i, j];
                    intcelule_adiacente = 1;
 67
                    if(i > 0)
                    {
                        apa_totala += nivel_apa[i -1, j];
                        celule_adiacente++;
                    }
                    if(i < marime_panou -1)
                    {
                        apa_totala += nivel_apa[i + 1, j];
                        celule_adiacente++;
                    }
                    if(j > 0)
                    {
                        apa_totala += nivel_apa[i, j -1];
                        celule_adiacente++;
                    }
                    if(j < marime_panou -1)
                    {
                        apa_totala += nivel_apa[i, j + 1];
                        celule_adiacente++;
                    }
                    nivel_apa_urm[i, j] = apa_totala / celule_adiacente;
                }
            }
            nivel_apa = nivel_apa_urm;
        }
        privatevoidDrawWater()
        {
            for(inti = 0; i < marime_panou; i++)
 68
            {
                for(intj = 0; j < marime_panou; j++)
                {
                    intcolorValue = (int)(nivel_apa[i, j] * 255);
                    panou_apa[i, j].BackColor = Color.FromArgb(colorValue, 
colorValue, 255);
                }
            }
        }
        privatevoidlabel4_Click(objectsender, EventArgs e)
        {
        }
    }
 16. Simularea propagării sunetului în mediu
 Acest cod simulează propagarea sunetului în aer folosind o 
rețea de butoane pentru a reprezenta intensitatea sunetului în 
diferite locații.
 În cadrul constructorului, se inițializează intervalul 
timerului și rețeaua de butoane. De asemenea, se stabilește 
poziția centrală a sunetului în rețeaua de butoane.
 Funcția intensitate calculează intensitatea sunetului în 
fiecare locație a rețelei de butoane bazându-se pe distanța 
față de centrul sunetului și utilizând funcția sinus pentru a 
simula variația intensității în funcție de distanță.
 Funcția deseneaza_Sunet colorează butoanele corespunzătoare 
locațiilor în funcție de intensitatea sunetului calculată 
anterior. Cu cât intensitatea sunetului este mai mare, cu atât 
culoarea butonului asociat va fi mai închisă.
 Timerul timer1 declanșează actualizarea și desenarea stării 
sunetului în rețeaua de butoane la fiecare interval de timp 
69
specificat.
 publicpartialclassitem17: Form
 {
    private constintpanou = 20;
    privateButton[,] panou_m = newButton[panou, panou];
    private double[,] intensityGrid = newdouble[panou, panou];
    private intcenterX, centerY;
    publicitem17()
    {
        InitializeComponent();
        timer1.Interval = 1000;
        panou_m_p();
        centerX = panou / 6;
        centerY = panou / 2;
    }
    private voidpanou_m_p()
    {
        for(inti = 0; i < panou; i++)
        {
            for(intj = 0; j < panou; j++)
            {
                Button button = newButton
                {
                    Size = newSize(30, 30),
                    Location = newPoint(i * 30, j * 30),
                    BackColor = Color.White,
                    FlatStyle = FlatStyle.Flat
                };
                panou_m[i, j] = button;
 70
                Controls.Add(button);
            }
        }
    }
    private voidintensitate()
    {
        for(inti = 0; i < panou; i++)
        {
            for(intj = 0; j < panou; j++)
            {
                doubledistance = Math.Sqrt(Math.Pow(i -centerX, 2) + 
Math.Pow(j -centerY, 2));
                intensityGrid[i, j] = Math.Sin(distance * 0.1) * 0.5 + 0.5;
            }
        }
    }
    private voiddeseneaza_Sunet()
    {
        for(inti = 0; i < panou; i++)
        {
            for(intj = 0; j < panou; j++)
            {
                intculoare = (int)(intensityGrid[i,j] * 255);
                panou_m[i, j].BackColor = Color.FromArgb(culoare, culoare, 
culoare);
            }
        }
        panou_m[centerX, centerY].BackColor = Color.Black;
    }
 71
    private voidtimer1_Tick(objectsender, EventArgs e)
    {
        intensitate();
        deseneaza_Sunet();
    }
    private voiditem17_Shown(objectsender, EventArgs e)
    {
        timer1.Start();
    }
 }
 17. Algoritmul Lee
 La început, aplicația inițializează o rețea de butoane care 
reprezintă matricea în care se va face căutarea drumului. 
Utilizatorul poate specifica dimensiunea matricei folosind un 
control NumericUpDown. După ce utilizatorul a selectat 
dimensiunea matricei și a apăsat butonul "Start", se afișează 
matricea de butoane și utilizatorul poate alege două puncte: 
punctul de start și punctul de sfârșit.
 Apăsarea butonului "Start" începe căutarea drumului folosind 
algoritmul Lee. Acest algoritm folosește o coadă pentru a 
explora toate celulele adiacente începând cu celula de start și 
înregistrând distanța față de celula de start în matricea c. 
Când algoritmul găsește celula de sfârșit, se oprește, iar 
drumul cel mai scurt este marcat cu culoarea verde pe butoanele 
respective.
 Butonul "Obstacole" permite utilizatorului să marcheze celulele 
matricei ca obstacole, iar butonul "Reset" resetează selecția 
punctelor de start și de sfârșit pentru a permite 
utilizatorului să selecteze alte puncte.
 publicpartialclassitem18: Form
 {
     intn, i = 0, j = 0, ip = 0, jp = 0, iso = 0, jso = 0, p = 1, u = 1, d, KK = 
72
0, kp = 1, nr = 0, KK2 = 0, ifn, jfn, iv, jv;
     Random r = newRandom();
     publicButton[,] a = newButton[16, 16];
     publicint[,] a1 = newint[15, 15];
     publicint[,] c = newint[115, 115];
     publicint[] di = newint[] { -1, 0, 1, 0 };
     publicint[] dj = newint[] { 0, 1, 0, -1 };
     publicint[] px = newint[115];
     publicint[] py = newint[115];
     intxb, yb;
     publicitem18()
     {
         InitializeComponent();
     }
     privatevoidbutton1_Click(objectsender, EventArgs e)
     {
         inti, j;
         n = int.Parse(numericUpDown1.Value.ToString());
         for(i = 0; i < n; i++)
             for(j = 0; j < n; j++)
                 a1[i, j] = 0;
         intk = 10 -n;
         for(i = 0; i < n; i++)
             for(j = 0; j < n; j++)
             {
                 a[i, j] = newButton();
                 a[i, j].Height = 50;
                 a[i, j].Width = 50;
 73
                 a[i, j].Text = "";
                 a[i, j].Name = i + " "+ j;
                 a[i, j].BackColor = Color.Gray;
                 a[i, j].Tag = Convert.ToString(n * i + j);
                 a[i, j].Location = newPoint(((k * 50) / 2) + i * 50, 100 + j * 
50);
                 a[i, j].Click += newEventHandler(v_click);
                 this.Controls.Add(a[i, j]);
             }
         button1.Visible = false;
         numericUpDown1.Visible = false;
         KK++;
     }
     boolOK(inti, intj)
     {
         if(i < 0 || j < 0 || i > n -1 || j > n -1)
             returnfalse;
         if(a1[i, j] == -1) returnfalse;
         if(c[i, j] != 0) returnfalse;
         if(i == iso && j == jso) returnfalse;
         returntrue;
     }
     boolultimul()
     {
         if(iv == ifn && jv == jfn)
             returntrue;
 74
         returnfalse;
     }
     privatevoidtimer1_Tick(objectsender, EventArgs e)
     {
         i = 0; j = 0;
         if(!(p <= u && a1[i, j] == 0) || ultimul() == true)
         {
             a[ifn, jfn].BackColor = Color.Yellow;
             a[ip, jp].BackColor = Color.Yellow;
             timer1.Stop();
             button4.Visible = false;
         }
         else
         {
             if(i < n)
                 if(j < n)
                     if(a1[i, j] == 0)
                         if(d < 4)
                         {
                             iv = px[p] + di[d];
                             jv = py[p] + dj[d];
                             d++;
 75
                             if(OK(iv, jv) == true)
                             {
                                 a[iv, jv].BackColor = Color.Green;
                                 u++;
                                 px[u] = iv; py[u] = jv;
                                 c[px[u], py[u]] = c[px[p], py[p]] + 1;
                                 a[iv, jv].Text = c[iv, jv].ToString();
                             }
                             if(OK(iv, jv) == true&& a[iv, jv].BackColor == 
Color.Black)
                                 nr++;
                         }
                         else{ d = 0; p++; }
                     elsej++;
                 else{ j = 0; i++; }
         }
     }
     privatevoidbutton4_Click(objectsender, EventArgs e)
     {
         if(KK2 == 0)
 76
         {
             for(i = 0; i < n; i++)
                 for(j = 0; j < n; j++)
                     a[i, j].Click += null;
             px[1] = ip;
             py[1] = jp;
             c[px[1], py[1]] = 1;
             timer1.Start();
             if(a[0, 0].BackColor == Color.Gray)
             {
                 a[0, 0].BackColor = Color.Black;
             }
             KK2++;
             button4.Text = "Programul";
             button4.Enabled = false;
         }
         else
         {
             //Form36 f = new Form36();
             //f.Show();
         }
     }
     privatevoidbutton3_Click(objectsender, EventArgs e)
     {
         if(kp == 1)
         {
             MessageBox.Show("Nu ai selectat locatie");
 77
         }
         else
         {
             KK++;
             xb = 0;
             yb = 0;
             kp = 1;
             MessageBox.Show("Pune obstacole");
             button3.Visible = false;
             button4.Visible = true;
         }
     }
     privatevoidbutton2_Click(objectsender, EventArgs e)
     {
         if(kp == 1)
         {
             MessageBox.Show("Nu ai selectat locatie");
         }
         else
         {
             KK++;
             xb = 0;
             yb = 0;
             kp = 1;
             MessageBox.Show("Alege urmatorul punct");
             button2.Visible = false;
             button3.Visible = true;
         }
 78
     }
     publicvoidv_click(objectsender, EventArgs e)
     {
         strings;
         string[] ss = newstring[2];
         Button btn = (Button)sender;
         if(KK == 3)
         {
             inti1, j1;
             intnrb = Convert.ToInt32(((Button)sender).Tag);
             i1 = nrb / n;
             j1 = nrb % n;
             if(a[i1, j1].BackColor != Color.White)
             {
                 a[i1, j1].BackColor = Color.Black;
                 a1[i1, j1] = -1;
             }
         }
         if(KK == 1)
         {
             if(a[xb, yb].BackColor == Color.White && kp == 0)
             {
                 a[xb, yb].BackColor = Color.Gray;
             }
 79
             s = btn.Name;
             ss = s.Split(' ');
             xb = int.Parse(ss[0]);
             yb = int.Parse(ss[1]);
             ip = xb;
             jp = yb;
             kp = 0;
             btn.BackColor = Color.White;
         }
         if(KK == 2)
         {
             if(a[xb, yb].BackColor == Color.White && kp == 0)
             {
                 a[xb, yb].BackColor = Color.Gray;
             }
             s = btn.Name;
             ss = s.Split(' ');
             xb = int.Parse(ss[0]);
             yb = int.Parse(ss[1]);
             ifn = xb;
             jfn = yb;
             kp = 0;
             btn.BackColor = Color.White;
         }
 80
}
 }
 18. Quiz 1
 Inițializarea quiz-ului: În constructorul clasei quiz1, se încarcă întrebările și răspunsurile din 
fișierul text utilizând metoda IncarcaIntrebarile. Apoi, se afișează prima întrebare utilizând 
metoda AfiseazaIntrebare.
 Încărcarea întrebărilor: Metoda IncarcaIntrebarile citește linie cu linie din fișierul text și 
împarte fiecare linie în întrebare și răspunsuri utilizând caracterul '/' pentru întrebare și 
caracterul ';' pentru răspunsuri. Aceste informații sunt stocate în tablourile intrebari și 
raspunsuri.
 Afișarea întrebării curente: Metoda AfiseazaIntrebare primește un index și afișează 
întrebarea corespunzătoare din tablourile intrebari și raspunsuri. Răspunsurile sunt afișate 
pe butoane radio pentru a permite utilizatorului să selecteze un răspuns.
 Verificarea răspunsului: În metoda button1_Click, se verifică dacă utilizatorul a selectat un 
răspuns înainte de a trece la următoarea întrebare. Dacă da, se apelează metoda 
VerificaRaspuns pentru a verifica dacă răspunsul este corect și se actualizează scorul. Apoi, 
se trece la următoarea întrebare sau se afișează un mesaj cu scorul final dacă nu mai sunt 
întrebări disponibile.
 Verificarea corectitudinii răspunsului: Metoda VerificaRaspuns compară răspunsul selectat 
de utilizator cu răspunsul corect stocat în tabloul raspunsuri și incrementează scorul dacă 
răspunsul este corect.
 public partial class quiz1 : Form
 {
 private string[] intrebari;
 private string[][] raspunsuri;
 private int intrebareCurenta;
 private int scor;
 public quiz1()
 {
 InitializeComponent();
 81
        IncarcaIntrebarile("quiz1.txt");
        AfiseazaIntrebare(intrebareCurenta);
    }
    private voidIncarcaIntrebarile(stringnumeFisier)
    {
        try
        {
            string[] linii = File.ReadAllLines(numeFisier);
            intrebari = newstring[linii.Length];
            raspunsuri = newstring[linii.Length][];
            for(inti = 0; i < linii.Length; i++)
            {
                string[] componente = linii[i].Split('/');
                intrebari[i] = componente[0];
                raspunsuri[i] = componente[1].Split(';');
            }
        }
        catch(Exception ex)
        {
            MessageBox.Show("Eroare la citirea fisierului: "+ ex.Message);
        }
    }
    private voidAfiseazaIntrebare(intindex)
    {
        if(index >= 0 && index < intrebari.Length)
        {
            label4.Text = intrebari[index];
 82
            radioButton1.Text = raspunsuri[index][0];
            radioButton2.Text = raspunsuri[index][1];
            radioButton3.Text = raspunsuri[index][2];
        }
        else
        {
            MessageBox.Show("Indexul intrebarii este invalid.");
        }
    }
    private voidquiz1_Load(objectsender, EventArgs e)
    {
    }
    private voidbutton1_Click(objectsender, EventArgs e)
    {
        if(radioButton1.Checked || radioButton2.Checked || radioButton3.Checked)
        {
            VerificaRaspuns();
            intrebareCurenta++;
            if(intrebareCurenta < intrebari.Length)
            {
                AfiseazaIntrebare(intrebareCurenta);
                radioButton1.Checked = radioButton2.Checked = 
radioButton3.Checked = false;
            }
            else
            {
                MessageBox.Show($"Ai raspuns corect la {scor}intrebari din 
{intrebari.Length}.");
 83
            }
        }
        else
        {
            MessageBox.Show("Selecteazăun răspuns înainte de a trece la 
următoarea întrebare.");
        }
    }
    private voidVerificaRaspuns()
    {
        stringraspunsCorect = raspunsuri[intrebareCurenta][3];
        if((radioButton1.Checked && radioButton1.Text == raspunsCorect) ||
            (radioButton2.Checked && radioButton2.Text == raspunsCorect) ||
            (radioButton3.Checked && radioButton3.Text == raspunsCorect))
        {
            scor++;
        }
    }
 }
 19. Quiz 2
 Inițializarea quiz-ului: În constructorul clasei quiz2, se 
încarcă întrebările și răspunsurile din fișierul text utilizând 
metoda CitesteEnunturiSiRaspunsuri, apoi se generează interfața 
utilizând metoda GenerareInterfata.
 Citirea întrebărilor și răspunsurilor: Metoda 
CitesteEnunturiSiRaspunsuri citește fișierul text linie cu 
linie și împarte fiecare linie în întrebare și răspunsuri, 
stocând aceste informații într-o listă de șiruri de caractere.
 Generarea interfeței grafice: Metoda GenerareInterfata creează 
o etichetă și un câmp text pentru fiecare întrebare și le 
adaugă în fereastra quiz-ului. De asemenea, adaugă un buton 
pentru verificarea răspunsurilor și stabilește evenimentul de 
84
click al acestuia pentru a apela metoda VerificaRaspunsuri.
 Verificarea răspunsurilor: În metoda VerificaRaspunsuri, se 
parcurg toate întrebările și se compară răspunsurile 
utilizatorului cu cele corecte. Dacă un răspuns este corect, 
eticheta corespunzătoare devine verde, altfel devine roșie. Se 
calculează și se afișează scorul final.
 Redimensionarea interfeței grafice: Metoda 
RedimensionareInterfata se ocupă de redimensionarea elementelor 
interfeței grafice atunci când fereastra quiz-ului este 
redimensionată.
 publicpartialclassquiz2: Form
 {
    privateList<string[]> enunturiSiRaspunsuri = newList<string[]>();
    privateList<System.Windows.Forms.TextBox> textBoxes = new
 List<System.Windows.Forms.TextBox>();
    privateList<Label> labels = newList<Label>();
    privateFont fontEnunt = newFont("Arial", 14, FontStyle.Regular);
    privateFont fontRaspuns = newFont("Arial", 12, FontStyle.Regular);
    private voidbutton1_Click(objectsender, EventArgs e)
    {
            
    }
    int[] vf = newint[100];
    publicquiz2()
    {
        InitializeComponent();
        CitesteEnunturiSiRaspunsuri("quiz2.txt");
        GenerareInterfata();
    }
    private voidCitesteEnunturiSiRaspunsuri(stringnumeFisier)
    {
 85
        try
        {
            string[] linii = File.ReadAllLines(numeFisier);
            foreach(stringlinie inlinii)
            {
                string[] enuntSiRaspunsuri = linie.Split('/');
                enunturiSiRaspunsuri.Add(enuntSiRaspunsuri);
            }
        }
        catch(IOException e)
        {
            MessageBox.Show("Eroare la citirea fișierului: "+ e.Message);
        }
    }
    private voidGenerareInterfata()
    {
        intyOffset = 50;
        foreach(string[] enuntSiRaspunsuri inenunturiSiRaspunsuri)
        {
            Label label = newLabel();
            label.Text = enuntSiRaspunsuri[0];
            label.Font = fontEnunt;
            label.AutoSize = true;
            label.Location = newPoint(50, yOffset);
            labels.Add(label);
            this.Controls.Add(label);
            System.Windows.Forms.TextBox textBox = new
 System.Windows.Forms.TextBox();
 86
            textBox.Font = fontRaspuns;
            textBox.Location = newPoint(50 + label.Width + 10, yOffset -3);
            textBox.Width = this.ClientSize.Width -label.Width -100;
            textBoxes.Add(textBox);
            this.Controls.Add(textBox);
            yOffset += 40;
        }
        System.Windows.Forms.Button verificareButton = new
 System.Windows.Forms.Button();
        verificareButton.Text = "Verificărăspunsurile";
        verificareButton.Size = newSize(120, 50);
        verificareButton.BackColor = Color.MediumPurple;
        verificareButton.Font = fontEnunt;
        verificareButton.Location = newPoint(this.Width / 2 
verificareButton.Width / 2, this.Height -verificareButton.Height * 2);
        verificareButton.Click += VerificaRaspunsuri;
        this.Controls.Add(verificareButton);
        this.Resize += quiz2_Resize;
    }
    private voidVerificaRaspunsuri(objectsender, EventArgs e)
    {
        intscor = 0;
        for(inti = 0; i < enunturiSiRaspunsuri.Count; i++)
        {
            string[] raspunsuriCorecte = 
enunturiSiRaspunsuri[i].Skip(1).ToArray();
            stringraspunsUtilizator = textBoxes[i].Text.Trim();
 87
            if(raspunsuriCorecte.Contains(raspunsUtilizator))
            {
                labels[i].ForeColor = Color.Green;
                scor++;
            }
            else
            {
                labels[i].ForeColor = Color.Red;
            }
        }
        MessageBox.Show("Scorul tău este: "+ scor + " din "+ 
enunturiSiRaspunsuri.Count);
        this.Close();
    }
    private voidquiz2_Load(objectsender, EventArgs e)
    {
        RedimensionareInterfata();
    }
    private voidRedimensionareInterfata()
    {
        for(inti = 0; i < enunturiSiRaspunsuri.Count; i++)
        {
            labels[i].Location = newPoint(50, 50 + 40 * i);
            textBoxes[i].Location = newPoint(50 + labels[i].Width + 10, 50 + 40 
* i -3);
            textBoxes[i].Width = this.ClientSize.Width -labels[i].Width -100;
        }
    }
 88
    private voidquiz2_Resize(objectsender, EventArgs e)
    {
        RedimensionareInterfata();
    }
 }
 20. Quiz 3
 Inițializare și încărcare întrebări: În constructorul clasei 
quiz3, se leagă evenimentele de click ale butoanelor "Adevărat" 
și "Fals" la metoda verifica_raspuns. Apoi, în metoda button2
 _Click, se încarcă întrebările și răspunsurile din fișierul 
text quiz3.txt și se afișează prima întrebare.
 Verificarea răspunsurilor: În metoda verifica_raspuns, se 
verifică răspunsul selectat de utilizator. Dacă răspunsul este 
corect, scorul este incrementat. Apoi se afișează următoarea 
întrebare sau, dacă utilizatorul a răspuns la toate 
întrebările, se afișează scorul final.
 Afișarea întrebărilor: Metoda scrie_intrebarea afișează 
întrebarea curentă pe eticheta label4.
 publicpartialclassquiz3: Form
 {
    stringraspuns;
    intn1 = 0;
    intn_intrebare = 0;
    intscor = 0;
    int[] v1 = newint[100];
    System.Windows.Forms.CheckBox[] c = newSystem.Windows.Forms.CheckBox[10];
    int[] v = newint[100];
    strings;
    Class3[] vect = newClass3[100];
    voidverificare()
    {
 89
            
    }
    publicquiz3()
    {
        InitializeComponent();
        button1.Click += verifica_raspuns;
        button4.Click += verifica_raspuns;
    }
    private voidquiz3_Shown(objectsender, EventArgs e)
    {
            
    }
    private voidverifica_raspuns(objectsender, EventArgs e)
    {
        Button buton_apasat = sender asButton;
        if(buton_apasat.Text == "Adevărat")
        {
            raspuns = "da";
        }
        else
        {
            raspuns = "nu";
        }
        if(raspuns == vect[n_intrebare].raspuns)
        {
            scor++;
        }
        n_intrebare++;
 90
        if(n_intrebare < n1)
        {
            scrie_intrebarea();
        }
        else
        {
            label4.Text = "Ai răspuns corect la "+ scor + " din "+ n1 + " 
întrebări";
            button1.Visible = false;
            button4.Visible = false;
        }
    }
    private voidscrie_intrebarea()
    {
        label4.Text = vect[n_intrebare].test;
    }
    private voidbutton2_Click(objectsender, EventArgs e)
    {
        button2.Visible = false;
        label4.Visible = true;
        button1.Visible = true;
        button4.Visible = true;
        using(StreamReader str = newStreamReader("quiz3.txt"))
        {
            stringlinie;
            while((linie = str.ReadLine()) != null)
            {
                vect[n1] = newClass3();
                vect[n1].test = linie;
 91
                vect[n1].raspuns = str.ReadLine();
                n1++;
            }
        }
        scrie_intrebarea();
    }
 }
 21. X și 0
 Inițializarea tabelului: În metoda InitializeazaTabla, se 
creează și se plasează butoanele pentru tabelul X și O pe 
fereastră. Aceste butoane sunt aranjate într-o matrice 3x3.
 Acțiunea de clic pe buton: Când un utilizator face clic pe un 
buton, metoda Buton_Click este activată. În această metodă, 
dacă jocul nu s-a încheiat încă, butonul pe care utilizatorul a 
făcut clic primește textul jucătorului curent (X sau O) și este 
dezactivat. Apoi, este verificat dacă un jucător a câștigat sau 
dacă este remiză, iar dacă nu, se trece la următorul jucător 
sau la mișcarea botului.
 Mișcare bot: Metoda MiscareBot este responsabilă pentru 
mișcarea botului. În această metodă, botul analizează tabla și 
alege mișcarea optimă pentru a câștiga sau a bloca un adversar. 
Dacă nu există o mișcare strategică imediată, botul alege o 
mișcare aleatoare.
 Verificarea câștigătorului: Metoda VerificaCastig este folosită 
pentru a verifica dacă un jucător a câștigat. Ea verifică 
liniile, coloanele și diagonalele pentru a vedea dacă toate 
butoanele de pe acea linie/coloană/diagonală sunt ocupate de 
același jucător.
 Verificarea remizei: Metoda VerificaRemiza este folosită pentru 
a verifica dacă jocul s-a terminat cu remiză. Dacă toate 
butoanele sunt ocupate și niciun jucător nu a câștigat, atunci 
jocul se încheie cu remiză.
 Resetarea jocului: Metoda Reseteaza este folosită pentru a 
reseta tabla și a începe un nou joc.
 92
publicpartialclassx_0: Form
 {
    privateButton[,] tabla;
    private charjucatorCurent;
    private booljocTerminat;
    publicx_0()
    {
        InitializeComponent();
        InitializeazaTabla();
        jucatorCurent = 'X';
        jocTerminat = false;
    }
    private voidInitializeazaTabla()
    {
        const intmarime = 3;
        const intmarimeButon = 100;
        const intpadding = 5;
        tabla = newButton[marime, marime];
        for(inti = 0; i < marime; i++)
        {
            for(intj = 0; j < marime; j++)
            {
                Button buton = newButton
                {
                    BackColor = Color.Indigo,
                    Size = newSystem.Drawing.Size(marimeButon, marimeButon),
                    Location = newSystem.Drawing.Point(j * (marimeButon + 
padding) + 30, i * (marimeButon + padding) + 60),
 93
                    Font = newSystem.Drawing.Font("Arial", 36F, 
System.Drawing.FontStyle.Bold, System.Drawing.GraphicsUnit.Point, ((byte)(0))),
                    Tag = newSystem.Drawing.Point(i, j),
                    TextAlign = System.Drawing.ContentAlignment.MiddleCenter,
                    Enabled = true
                };
                buton.Click += Buton_Click;
                Controls.Add(buton);
                tabla[i, j] = buton;
            }
        }
    }
    private voidButon_Click(objectsender, EventArgs e)
    {
        if(jocTerminat) return;
        Button buton = (Button)sender;
        buton.Text = jucatorCurent.ToString();
        buton.Enabled = false;
        intrand = ((System.Drawing.Point)buton.Tag).X;
        intcoloana = ((System.Drawing.Point)buton.Tag).Y;
        if(VerificaCastig(rand, coloana, jucatorCurent))
        {
            MessageBox.Show($"Jucătorul {jucatorCurent}a câștigat!"); //trebuie 
schimbat cu un label
            jocTerminat = true;
            Reseteaza();
        }
 94
        elseif(VerificaRemiza())
        {
            MessageBox.Show("E remiză!"); //trebuie schimbat cu un label si asta
            jocTerminat = true;
            Reseteaza();
        }
        else
        {
            jucatorCurent = (jucatorCurent == 'X') ? 'O': 'X';
            if(jucatorCurent == 'O')
            {
                MiscareBot();
            }
        }
    }
    private voidMiscareBot()
    {
        int[] miscare = AlegeMiscareOptima();
        tabla[miscare[0], miscare[1]].PerformClick();
    }
    private int[] AlegeMiscareOptima()
    {
        //MERGEEEEEEEEEEE
        for(inti = 0; i < 3; i++)
        {
            for(intj = 0; j < 3; j++)
            {
                if(tabla[i, j].Text == "")
                {
 95
                    tabla[i, j].Text = "O";
                    if(VerificaCastig(i, j, 'O'))
                    {
                        tabla[i, j].Text = "";
                        returnnewint[] { i, j };
                    }
                    tabla[i, j].Text = "";
                }
            }
        }
        for(inti = 0; i < 3; i++)
        {
            for(intj = 0; j < 3; j++)
            {
                if(tabla[i, j].Text == "")
                {
                    tabla[i, j].Text = "X";
                    if(VerificaCastig(i, j, 'X'))
                    {
                        tabla[i, j].Text = "";
                        returnnewint[] { i, j };
                    }
                    tabla[i, j].Text = "";
                }
            }
        }
        List<int[]> pozitiiStrategice = newList<int[]>
 96
        {
            newint[] { 1, 1 }, 
            newint[] { 0, 0 }, 
            newint[] { 0, 2 },
            newint[] { 2, 0 },
            newint[] { 2, 2 }
        };
        Random random = newRandom();
        foreach(var pozitie inpozitiiStrategice.OrderBy(x => random.Next()))
        {
            if(tabla[pozitie[0], pozitie[1]].Text == "")
            {
                returnpozitie;
            }
        }
        List<int[]> pozitiiLibere = newList<int[]>();
        for(inti = 0; i < 3; i++)
        {
            for(intj = 0; j < 3; j++)
            {
                if(tabla[i, j].Text == "")
                {
                    pozitiiLibere.Add(newint[] { i, j });
                }
            }
        }
        returnpozitiiLibere[random.Next(pozitiiLibere.Count)];
 97
    }
    private boolVerificaCastig(intrand, intcoloana, charjucator)
    {
        for(inti = 0; i < 3; i++)
        {
            if(tabla[rand, i].Text != jucator.ToString()) break;
            if(i == 2) returntrue;
        }
        for(inti = 0; i < 3; i++)
        {
            if(tabla[i, coloana].Text != jucator.ToString()) break;
            if(i == 2) returntrue;
        }
        if(rand == coloana)
        {
            for(inti = 0; i < 3; i++)
            {
                if(tabla[i, i].Text != jucator.ToString()) break;
                if(i == 2) returntrue;
            }
        }
        if(rand + coloana == 2)
        {
            for(inti = 0; i < 3; i++)
 98
            {
                if(tabla[i, 2 -i].Text != jucator.ToString()) break;
                if(i == 2) returntrue;
            }
        }
        returnfalse;
    }
    private boolVerificaRemiza()
    {
        foreach(Button buton intabla)
        {
            if(buton.Text == "") returnfalse;
        }
        returntrue;
    }
    private voidReseteaza()
    {
        foreach(Button buton intabla)
        {
            buton.Text = "";
            buton.Enabled = true;
        }
        jucatorCurent = 'X';
        jocTerminat = false;
    }
    private voidx_0_Load(objectsender, EventArgs e)
    {
 99
}
 }
 22. Puzzle
 OpenFileEvent: Această funcție se activează atunci când 
utilizatorul dorește să deschidă o imagine pentru a o folosi în 
joc. Utilizatorul poate selecta un fișier de imagine, iar apoi 
imaginea este încărcată și afișată în fereastra de joc.
 CreazaImagini: Această funcție creează 9 imagini mici din 
imaginea principală, fiecare imagine mică reprezentând o bucată 
a puzzle-ului. Aceste imagini sunt stocate într-o listă de 
imagini.
 OnPicClick: Această funcție este activată atunci când 
utilizatorul face clic pe o imagine mică din puzzle. Dacă 
imaginea mică pe care a făcut clic utilizatorul este vecină cu 
imaginea goală, atunci cele două imagini sunt interschimbate, 
permițând astfel mutarea bucății puzzle-ului. Apoi, funcția 
verifică dacă imaginea este plasată în poziția corectă pentru a 
rezolva puzzle-ul.
 CropImage: Această funcție taie imaginea principală în bucăți 
mai mici, fiecare reprezentând o bucată a puzzle-ului. 
Imaginile tăiate sunt adăugate într-o listă de imagini.
 AdaugaImagini: Această funcție adaugă imaginile tăiate la 
controalele PictureBox din formular și le plasează aleatoriu pe 
ecran pentru a începe jocul.
 PlacePictureBoxesToForm: Această funcție plasează controalele 
PictureBox pe formular și stabilește pozițiile lor inițiale pe 
ecran.
 CheckGame: Această funcție verifică dacă poziția curentă a 
bucăților de puzzle este identică cu poziția corectă pentru a 
rezolva puzzle-ul. Dacă poziția este corectă, se afișează un 
mesaj de felicitare și jocul este încheiat.
 public partial class puzzle : Form
 {
 private int miscariEfectuate = 0;
 100
    List<PictureBox> listaPictureBox = newList<PictureBox>();
    List<Bitmap> imagini = newList<Bitmap>();
    List<string> locatii = newList<string>();
    List<string> locatiiCurente = newList<string>();
    stringpozitieCastig;
    stringpozitieCurenta;
    Bitmap imaginePrincipala;
    private intsecunde, minut;
    publicpuzzle()
    {
        InitializeComponent();
        timer1.Interval = 1000;
    }
    private voidOpenFileEvent(objectsender, EventArgs e)
    {
        if(listaPictureBox != null)
        {
            foreach(PictureBox pictureBox inlistaPictureBox.ToList())
            {
                this.Controls.Remove(pictureBox);
            }
            listaPictureBox.Clear();
            imagini.Clear();
            locatii.Clear();
            locatiiCurente.Clear();
            pozitieCastig = string.Empty;
 101
            pozitieCurenta = string.Empty;
        }
        OpenFileDialog open = newOpenFileDialog();
        open.Filter = "Image Files Only | *.jpg; *.jpeg; *.gif; *.png";
        if(open.ShowDialog() == DialogResult.OK)
        {
            imaginePrincipala = newBitmap(open.FileName);
            CreazaImagini();
            AdaugaImagini();
            timer1.Start();
        }
    }
    private voidCreazaImagini()
    {
        for(inti = 0; i < 9; i++)
        {
            PictureBox pictureBoxTemp = newPictureBox();
            pictureBoxTemp.Size = newSize(130, 130);
            pictureBoxTemp.Tag = i.ToString();
            pictureBoxTemp.Click += OnPicClick;
            listaPictureBox.Add(pictureBoxTemp);
            locatii.Add(pictureBoxTemp.Tag.ToString());
        }
    }
    private voidOnPicClick(objectsender, EventArgs e)
 102
    {
        PictureBox pictureBoxApasat = (PictureBox)sender;
        PictureBox pictureBoxGol = listaPictureBox.Find(x => x.Tag.ToString() == 
"0");
        Point punct1 = newPoint(pictureBoxApasat.Location.X, 
pictureBoxApasat.Location.Y);
        Point punct2 = newPoint(pictureBoxGol.Location.X, 
pictureBoxGol.Location.Y);
        intindex1 = this.Controls.IndexOf(pictureBoxApasat);
        intindex2 = this.Controls.IndexOf(pictureBoxGol);
        if((pictureBoxApasat.Right == pictureBoxGol.Left && 
pictureBoxApasat.Location.Y == pictureBoxGol.Location.Y)
            || (pictureBoxApasat.Left == pictureBoxGol.Right && 
pictureBoxApasat.Location.Y == pictureBoxGol.Location.Y)
            || (pictureBoxApasat.Top == pictureBoxGol.Bottom && 
pictureBoxApasat.Location.X == pictureBoxGol.Location.X)
            || (pictureBoxApasat.Bottom == pictureBoxGol.Top && 
pictureBoxApasat.Location.X == pictureBoxGol.Location.X))
        {
            miscariEfectuate++;
            label1.Text = "Mișcări efectuate: "+ miscariEfectuate;
            pictureBoxApasat.Location = punct2;
            pictureBoxGol.Location = punct1;
            this.Controls.SetChildIndex(pictureBoxApasat, index2);
            this.Controls.SetChildIndex(pictureBoxGol, index1);
        }
        locatiiCurente.Clear();
        CheckGame();
    }
    private voidCropImage(Bitmap imaginePrincipala, intinaltime, intlatime)
 103
    {
        intx, y;
        x = 0;
        y = 0;
        for(intblocuri = 0; blocuri < 9; blocuri++)
        {
            Bitmap imagineTaiata = newBitmap(inaltime, latime);
            for(inti = 0; i < inaltime; i++)
            {
                for(intj = 0; j < latime; j++)
                {
                    imagineTaiata.SetPixel(i, j, imaginePrincipala.GetPixel((i + 
x), (j + y)));
                }
            }
            imagini.Add(imagineTaiata);
            x += 130;
            if(x == 390)
            {
                x = 0;
                y += 130;
            }
        }
    }
    private voidAdaugaImagini()
 104
    {
        Bitmap imagineTemporara = newBitmap(imaginePrincipala, newSize(390, 
390));
        CropImage(imagineTemporara, 130, 130);
        for(inti = 1; i < listaPictureBox.Count; i++)
        {
            listaPictureBox[i].BackgroundImage = (Image)imagini[i];
        }
        PlacePictureBoxesToForm();
    }
    private voidPlacePictureBoxesToForm()
    {
        varimaginiAmestecate = listaPictureBox.OrderBy(a => 
Guid.NewGuid()).ToList();
        listaPictureBox = imaginiAmestecate;
        intx = 50;
        inty = 15;
        for(inti = 0; i < listaPictureBox.Count; i++)
        {
            listaPictureBox[i].BackColor = Color.Purple;
            if(i == 3 || i == 6)
            {
                y += 130;
                x = 50;
            }
 105
            listaPictureBox[i].BorderStyle = BorderStyle.FixedSingle;
            listaPictureBox[i].Location = newPoint(x, y);
            this.Controls.Add(listaPictureBox[i]);
            x += 130;
            pozitieCastig += locatii[i];
        }
    }
    private voidCheckGame()
    {
        foreach(Control control inthis.Controls)
        {
            if(control isPictureBox pictureBox)
            {
                locatiiCurente.Add(pictureBox.Tag.ToString());
            }
        }
        stringpozitieCurenta = string.Join("", locatiiCurente);
        if(pozitieCastig == pozitieCurenta)
        {
            MessageBox.Show("Felicitări! Ai potrivit imaginea.");
            this.Close();
        }
    }
    private voidbutton1_Click(objectsender, EventArgs e)
    {
 106
        miscariEfectuate = 0;
        label1.Text = "Mișcări efectuate: ";
        if(listaPictureBox != null)
        {
            foreach(PictureBox pictureBox inlistaPictureBox.ToList())
            {
                this.Controls.Remove(pictureBox);
            }
            listaPictureBox.Clear();
            imagini.Clear();
            locatii.Clear();
            locatiiCurente.Clear();
            pozitieCastig = string.Empty;
            pozitieCurenta = string.Empty;
        }
        OpenFileDialog open = newOpenFileDialog();
        open.Filter = "Image Files Only | *.jpg; *.jpeg; *.gif; *.png";
        if(open.ShowDialog() == DialogResult.OK)
        {
            imaginePrincipala = newBitmap(open.FileName);
            CreazaImagini();
            AdaugaImagini();
        }
    }
 }
 23. Minesweeper
 107
Funcția PornesteJoc() inițializează jocul, creând butoane 
pentru fiecare căsuță a tabloului și configurându-le 
dimensiunea, locația și evenimentul de click.
 PlaseazaMine() este responsabilă de plasarea minelor pe tablă. 
Ea generează aleatoriu locațiile minelor și se asigură că 
acestea sunt distribuite uniform.
 Atunci când un jucător face clic pe o căsuță a tabloului, este 
activată funcția buton_Click(). Aceasta verifică dacă căsuța 
conține o mină sau nu și dezvăluie căsuțele goale din jurul 
acesteia, dacă este cazul.
 NumaraBombe(int x, int y): Numără câte mine sunt învecinate cu 
o anumită căsuță de la coordonatele (x, y).
 UmpleCeluleleGoale(int x, int y): Descoperă recursiv toate 
căsuțele goale din jurul unei căsuțe care a fost descoperită și 
care nu are mine în vecinătate.
 VerificaCastigat(): Verifică dacă toate căsuțele care nu conțin 
mine au fost descoperite, ceea ce înseamnă că jucătorul a 
câștigat jocul.
   private staticintnumarColoane = meniu_minesweeper.numarColoane;
    private static intnumarMine = meniu_minesweeper.numarMine;
    Color culoare;
    privateButton[,] panou = newButton[numarColoane, numarColoane];
    private bool[,] eMina = newbool[numarColoane, numarColoane];
    private intunrevealedNonBombCells;
    publicForm8()
    {
        InitializeComponent();
        PornesteJoc();
        this.Resize += Form8_Resize;
        PlaseazaMine();
        unrevealedNonBombCells = numarColoane * numarColoane -numarMine;
    }
 108
    private voidPornesteJoc()
    {
        const intbuttonSize = 30;
        const intpadding = 5;
        const intformMargin = 20;
        for(inti = 0; i < numarColoane; i++)
        {
            for(intj = 0; j < numarColoane; j++)
            {
                varbutton = newButton
                {
                    Size = newSize(buttonSize, buttonSize),
                    Location = newPoint(j * (buttonSize + padding), i * 
(buttonSize + padding)),
                    Tag = newPoint(i, j),
                    TextAlign = ContentAlignment.MiddleCenter,
                };
                if(eMina[i, j])
                {
                    button.Text = "";
                }
                button.Click += buton_Click;
                Controls.Add(button);
                panou[i, j] = button;
            }
        }
 109
        intformWidth = numarColoane * (buttonSize + padding) + formMargin;
        intformHeight = numarColoane * (buttonSize + padding) + formMargin;
        this.MinimumSize = newSize(formWidth, formHeight);
        Size = newSize(formWidth, formHeight);
    }
    private voidPlaseazaMine()
    {
        Random random = newRandom();
        for(inti = 0; i < numarMine; i++)
        {
            intx = random.Next(0, numarColoane);
            inty = random.Next(0, numarColoane);
            if(!eMina[x, y])
            {
                eMina[x, y] = true;
                panou[x, y].Text = "";
            }
            else
            {
                i--;
            }
        }
    }
    private voidbuton_Click(objectsender, EventArgs e)
    {
        Button button = (Button)sender;
        Point location = (Point)button.Tag;
 110
        intx = location.X;
        inty = location.Y;
        if(eMina[x, y])
        {
            DezvaluieMine();
            MessageBox.Show("Ai declanșat o bombă! Joc pierdut.");
            Reseteaza();
        }
        else
        {
            intbombCount = NumaraBombe(x, y);
            button.Text = bombCount.ToString();
            culoare =  culoareNumar(bombCount);
            button.ForeColor = culoare;
            button.Enabled = false;
            if(bombCount == 0)
            {
                UmpleCeluleleGoale(x, y);
            }
            if(VerificaCastigat())
            {
                MessageBox.Show("Felicitări! Ai câștigat.");
                Reseteaza();
            }
        }
    }
 111
    private voidDezvaluieMine()
    {
        for(inti = 0; i < numarColoane; i++)
        {
            for(intj = 0; j < numarColoane; j++)
            {
                if(eMina[i, j])
                {
                    panou[i, j].Text = "*";
                }
            }
        }
    }
    private intNumaraBombe(intx, inty)
    {
        intcount = 0;
        for(inti = Math.Max(0, x -1); i <= Math.Min(numarColoane -1, x + 1); 
i++)
        {
            for(intj = Math.Max(0, y -1); j <= Math.Min(numarColoane -1, y + 
1); j++)
            {
                if(eMina[i, j])
                {
                    count++;
                }
            }
        }
        returncount;
    }
 112
    private voidresizeText()
    {
        const intspatiu = 5;
        const intminMarimeButon = 30; 
        const intminMarimeFont = 8;
        const intmaxMarimeFont = 16;
        intmarimeButon = Math.Max(Math.Min((ClientSize.Width -(numarColoane + 
1) * spatiu) / numarColoane, (ClientSize.Height -(numarColoane + 1) * spatiu) / 
numarColoane), minMarimeButon);
        floatmarimeFont = Math.Max(Math.Min((float)marimeButon / 2, 
maxMarimeFont), minMarimeFont);
        Font font = newFont("Arial", marimeFont);
        foreach(Button buton inpanou)
        {
            buton.Font = font;
        }
    }
    private voidresizeButoane()
    {
        const intspatiu = 1;
        intmaxButtonSize = Math.Min((ClientSize.Width -(numarColoane + 1) * 
spatiu) / numarColoane, (ClientSize.Height -(numarColoane + 1) * spatiu) / 
numarColoane);
        intbuttonSize = Math.Max(maxButtonSize, 10);
        for(inti = 0; i < numarColoane; i++)
 113
        {
            for(intj = 0; j < numarColoane; j++)
            {
                varbutton = panou[i, j];
                button.Size = newSize(buttonSize, buttonSize);
                button.Location = newPoint(spatiu + j * (buttonSize + spatiu), 
spatiu + i * (buttonSize + spatiu));
            }
        }
    }
    private voidUmpleCeluleleGoale(intx, inty)
    {
        for(inti = Math.Max(0, x -1); i <= Math.Min(numarColoane -1, x + 1); 
i++)
        {
            for(intj = Math.Max(0, y -1); j <= Math.Min(numarColoane -1, y + 
1); j++)
            {
                if(panou[i, j].Enabled && NumaraBombe(i, j) == 0)
                {
                    panou[i, j].Enabled = false;
                    UmpleCeluleleGoale(i, j);
                }
                elseif(panou[i, j].Enabled)
                {
                    panou[i, j].Text = NumaraBombe(i, j).ToString();
                    panou[i, j].Enabled = false;
                }
            }
        }
    }
 114
    private boolVerificaCastigat()
    {
        for(inti = 0; i < numarColoane; i++)
        {
            for(intj = 0; j < numarColoane; j++)
            {
                if(!eMina[i, j] && panou[i, j].Enabled)
                {
                    returnfalse;
                }
            }
        }
        returntrue;
    }
    private voidReseteaza()
    {
        foreach(Button buton inpanou)
        {
            buton.Text = "";
            buton.Enabled = true;
        }
        Array.Clear(eMina, 0, eMina.Length);
        PlaseazaMine();
    }
    private voidForm8_Load(objectsender, EventArgs e)
    {
    }
 115
    private voidForm8_Resize(objectsender, EventArgs e)
    {
        resizeButoane();
        resizeText();
    }
    privateColor culoareNumar(intnumber)
    {
        switch(number)
        {
            case1:
                culoare = Color.Blue;
                returnculoare;
            case2:
                culoare = Color.Green;
                returnculoare;
            case3:
                culoare = Color.Red;
                returnculoare;
            case4:
                culoare = Color.DarkBlue;
                returnculoare;
            case5:
                culoare = Color.DarkRed;
                returnculoare;
            case6:
                culoare = Color.Blue;
                returnculoare;
            case7:
                culoare = Color.Blue;
 116
                returnculoare;
            default:
                culoare = Color.Blue;
                returnculoare;
        }
    }
 }
 117
