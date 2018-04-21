#include <iostream>

using namespace std;
class ListaDubluInlantuita
{
    public:

    ListaDubluInlantuita *inceput;
    int val;
    ListaDubluInlantuita *inainte;
    ListaDubluInlantuita *inapoi;



};
void afiseazaMeniuListaDubluInlantuita()
{
    cout<<"Aveti urmatoarele optiuni"<<endl;
    cout<<"1. Adaugarea unui element la inceput."<<endl;
    cout<<"2. Adaugarea unui element la sfarsit."<<endl;
    cout<<"3. Adaugarea unui element in interiorul listei."<<endl;
    cout<<"4. Afisarea elementelor listei in ordinea introducerii lor."<<endl;
    cout<<"5. Afisarea elementelor listei in ordine inversa."<<endl;
    cout<<"6. Stergerea unui element din lista stiind pozitia lui."<<endl;
    cout<<"7. Stergerea unui element din lista stiind valoarea lui."<<endl;
    cout<<"0 - EXIT"<<endl;
}

void adaugaElementInceput(ListaDubluInlantuita *&LDI)
{
    cout<<"Introduceti un numar :"<<endl;
    int nr;
    cin>>nr;

    if (LDI == NULL)
    {
        LDI = new ListaDubluInlantuita;
        LDI->val = nr;
        LDI->inainte = NULL;
        LDI->inapoi = NULL;
    }
    else
    {
        ListaDubluInlantuita *p;
        p = new ListaDubluInlantuita;
        p->val = nr;
        p->inainte = LDI;
        p->inapoi = NULL;
        LDI->inapoi = p;
        LDI = p;
    }
}

void adaugaElementSfarsit(ListaDubluInlantuita *&LDI)
{
    cout<<" Introduceti un numar: "<<endl;
    int nr;
    cin>>nr;

    if (LDI == NULL)
    {
        LDI = new ListaDubluInlantuita;
        LDI->val = nr;
        LDI->inainte = NULL;
        LDI->inapoi = NULL;
    }
    else
    {
        ListaDubluInlantuita *p;
        p = new ListaDubluInlantuita;
        p->val = nr;
        p->inainte = NULL;

        ListaDubluInlantuita *q;
        q = LDI;
        while (q->inainte)
            q = q->inainte;

        p->inapoi = q;
        q->inainte = p;
    }
}

void adaugaElementInterior(ListaDubluInlantuita *&LDI)
{
    cout<<"Introduceti un numar: "<<endl;
    int nr;
    cin>>nr;

    cout<<"Introduceti pozitia pe care sa fie inserat."<<endl;
    int poz;
    cin>>poz;

    if (poz == 1)
        cout<<"Pozitia este incorecta ! Elementul trebuie sa fie pus in interiorul listei."<<endl;
    else
    {
        if (LDI == NULL)
            cout<<"Lista este vida!"<<endl;
        else
        {
            ListaDubluInlantuita *p, *q;
            p = LDI;
            q = LDI->inainte;

            poz--;

            bool introdus = 0;
            while (q && poz && !introdus)
            {
                poz--;
                if (poz == 0)
                {
                    ListaDubluInlantuita *r;
                    r = new ListaDubluInlantuita;
                    r->val = nr;
                    r->inainte = q;
                    r->inapoi = p;
                    p->inainte = r;
                    q->inapoi = r;
                    introdus = 1;
                }
                q = q->inainte;
                p = p->inainte;
            }
            if (introdus == 0)
                cout<<"Elementul nu a fost introdus, pozitie incorecta!"<<endl;
        }
    }
}

void afisareaElementelorOrdine(ListaDubluInlantuita *&LDI)
{
    cout<<"Elementele listei in ordinea introducerii sunt:"<<endl;

    ListaDubluInlantuita *p;
    p = LDI;
    while (p)
    {
        cout<<p->val<<" ";
        p = p->inainte;
    }
    cout<<endl;
}

void afisareaElementelorOrdineInversa(ListaDubluInlantuita *&LDI)
{
    cout<<"Elementele listei in ordine inversa sunt:"<<endl;

    ListaDubluInlantuita *p;
    p = LDI;

    while (p->inainte)
        p = p->inainte;

    while (p)
    {
        cout<<p->val<<" ";
        p = p->inapoi;
    }
    cout<<endl;
}

void stergereElementNumarOrdine(ListaDubluInlantuita *&LDI)
{
    cout<<"Introduceti pozitia elementului care trebuie sters."<<endl;
    int poz;
    cin>>poz;

    if (poz < 1)
        cout<<"Pozitie incorecta"<<endl;
    if (poz == 1)
    {
        ListaDubluInlantuita *p = LDI;
        LDI = LDI->inainte;
        LDI->inapoi = NULL;
        delete p;
    }
    if (poz > 1)
    {
        ListaDubluInlantuita *p, *q;
        p = LDI;
        q = LDI->inainte;


        poz--;
        bool sters = 0;
        while (q && poz && !sters)
        {
            poz--;
            if (poz == 0)
            {
                p->inainte = q->inainte;
                if (q->inainte != NULL)
                    q->inainte->inapoi = p;

                delete q;
                sters = 1;
            }
            p = p->inainte;
            q = q->inainte;
        }
        if (sters == 0)
            cout<<"Elementul nu s-a sters, pozitie incorecta!"<<endl;
    }
}

void stergereElementValoare(ListaDubluInlantuita *&LDI)
{
    cout<<"Introduceti valoarea elementului care trebuie sters."<<endl;
    int valoare;
    cin>>valoare;

    if (LDI->val == valoare)
    {
        ListaDubluInlantuita *p = LDI;
        LDI = LDI->inainte;
        LDI->inapoi = NULL;
        delete p;
    }
    else
    {
        ListaDubluInlantuita *p, *q;
        p = LDI;
        q = LDI->inainte;

        bool sters = 0;
        while (q && q->val != valoare && !sters)
        {
            p = p->inainte;
            q = q->inainte;
        }
        if (q != NULL)
        {
            p->inainte = q->inainte;
            if (q->inainte != NULL)
                q->inainte->inapoi = p;

            delete q;
            sters = 1;
        }
        if (sters == 0)
            cout<<"Elementul nu a fost gasit in lista!"<<endl;
    }
}

void START()
{
    ListaDubluInlantuita *LDI = NULL;

    while (1)
    {
        int alegere;
        afiseazaMeniuListaDubluInlantuita();

        cout<<"Ce optiune alegeti?"<<endl;
        cin>>alegere;
        switch (alegere)
        {
            case 1 : adaugaElementInceput(LDI); break;
            case 2 : adaugaElementSfarsit(LDI); break;
            case 3 : adaugaElementInterior(LDI); break;
            case 4 : afisareaElementelorOrdine(LDI); break;
            case 5 : afisareaElementelorOrdineInversa(LDI); break;
            case 6 : stergereElementNumarOrdine(LDI); break;
            case 7 : stergereElementValoare(LDI); break;
        }

        cout<<endl;
        if (alegere == 0) break;
    }
}
int main()
{
    START();
}
