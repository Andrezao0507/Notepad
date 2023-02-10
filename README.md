# Notepad
 
unit Unit1;

interface

uses
  Winapi.Windows, Winapi.Messages, System.SysUtils, System.Variants, System.Classes, Vcl.Graphics,
  Vcl.Controls, Vcl.Forms, Vcl.Dialogs, Vcl.Menus, Vcl.ExtCtrls, Vcl.StdCtrls;

type
  TForm1 = class(TForm)
    Pnlconteiner: TPanel;
    PnlTop: TPanel;
    MainMenu1: TMainMenu;
    Arquivo1: TMenuItem;
    Arquivo2: TMenuItem;
    Abrir1: TMenuItem;
    Abrir2: TMenuItem;
    Salvar1: TMenuItem;
    Sair1: TMenuItem;
    Sair2: TMenuItem;
    Desfazer1: TMenuItem;
    Desfazer2: TMenuItem;
    Colar1: TMenuItem;
    Recortar1: TMenuItem;
    Pnlsalvar: TPanel;
    Shape5: TShape;
    btnsalvar: TButton;
    PnlEspaço: TPanel;
    Pnlabrir: TPanel;
    Shape1: TShape;
    Button1: TButton;
    PnlEspaço2: TPanel;
    Shape2: TShape;
    btnsair: TButton;
    PnlSair: TPanel;
    Memo: TMemo;
    Dlgabrir: TOpenDialog;
    DlgSalvar: TSaveDialog;
    N1: TMenuItem;
    Sobre1: TMenuItem;
    procedure btnsairClick(Sender: TObject);
    procedure Desfazer1Click(Sender: TObject);
    procedure Desfazer2Click(Sender: TObject);
    procedure Recortar1Click(Sender: TObject);
    procedure Colar1Click(Sender: TObject);
    procedure Sair1Click(Sender: TObject);
    procedure Abrir1Click(Sender: TObject);
    procedure Abrir2Click(Sender: TObject);
    procedure Salvar1Click(Sender: TObject);
    procedure Memochange(Sender: TObject);
    procedure Arquivo2Click(Sender: TObject);
    procedure Fromcreate(Sender: TObject);
    procedure Sobre1Click(Sender: TObject);
  private
    { Private declarations }
  public
    { Public declarations }
    bHouveAlteracoes: boolean;
    procedure pSalvar;
  end;

var
  Form1: TForm1;

implementation

{$R *.dfm}

uses Unit2;

procedure TForm1.Abrir1Click(Sender: TObject);
begin
  if dlgabrir.Execute  then
  begin
      memo.Lines.LoadFromFile(dlgabrir.FileName);
      BHouveAlteracoes:=False;
  end;
end;

procedure TForm1.Abrir2Click(Sender: TObject);
begin
  Memo.Lines.SaveToFile('notepad.txt');
  BHouveAlteracoes:=False;
end;

procedure TForm1.Arquivo2Click(Sender: TObject);
begin
if bHouveAlteracoes=false then
  begin

  case MessageDlg('Deseja Salvar?', mtConfirmation, [mbyes, mbno, mbcancel],0)  of
  mrcancel:
    begin
        bHouveAlteracoes:=False;
        Memo.Lines.Clear;
    end;
    mryes:
    begin
      pSalvar;
      Memo.Lines.Clear;
    end;
  end;
end
  else
    begin
      Memo.Lines.Clear;
    end;
end;

procedure TForm1.btnsairClick(Sender: TObject);
begin
 Application.Terminate;
end;

procedure TForm1.Colar1Click(Sender: TObject);
begin
  Memo.pastefromclipboard; {colar}
end;

procedure TForm1.Desfazer1Click(Sender: TObject);
begin
  Memo.Undo; {desfazer}
end;

procedure TForm1.Desfazer2Click(Sender: TObject);
begin
  Memo.CopyToClipboard {copiar}
end;

procedure TForm1.Fromcreate(Sender: TObject);
begin
  BHouveAlteracoes:=False;
end;

procedure TForm1.Memochange(Sender: TObject);
begin
  bHouveAlteracoes:=true;
end;

procedure TForm1.pSalvar;
begin
  if dlgSalvar.execute then
  begin
  Memo.Lines.SaveToFile(dlgsalvar.filename);
  bHouveAlteracoes:=False;
end;
end;

procedure TForm1.Recortar1Click(Sender: TObject);
begin
  Memo.CutToClipboard; {recortar}
end;

procedure TForm1.Sair1Click(Sender: TObject);
begin
  if not bHouveAlteracoes then
  Application.Terminate
  else
  if  MessageDlg('Deseja Salvar?', mtConfirmation, [mbyes, mbno, mbcancel],0) = mryes then
  begin
    pSalvar;
    Application.Terminate;
  end;

end;

procedure TForm1.Salvar1Click(Sender: TObject);
begin
  pSalvar;
end;

procedure TForm1.Sobre1Click(Sender: TObject);
begin
  Form2.show;
end;

end.
