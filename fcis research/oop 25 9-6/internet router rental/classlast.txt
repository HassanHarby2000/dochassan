
import javax.swing.JFrame;
import javax.xml.crypto.Data;
import java.util.concurrent.*; 
import java.util.Date; 
import java.awt.Graphics;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.io.Console;

import javax.swing.*;
import java.util.*;

 abstract class user{
private int userID ;
private String userName ;
private String Password;
private int age ;
private double money;
public user(int userID,String userName,String Password,int age,double money){
 this.Password= Password;
 this.userID = userID;
 this.userName = userName ;
 this.age = age ;
 this.money = money ;
}
public   void   setuserID (int userID ){this.userID=userID ;}
public   void   setuserName (String userName ){this.userName=userName ;}
public   void   setPassword(String Password){this.Password=Password ;}
public   void   setAge(int age){ this.age=age ;}
public   int    getAge(){ return age; }
public   int    getuserID(){ return userID ; }
public   String getuserName (){return userName   ;}
public   String getPassword(){return Password  ;}
public   void   setmoney(double money){ this.money=money ;}
public   double    getMoney(){ return money; }
public abstract  double payment( double fees );
}



// class Resident  
// --------------------------------
class Resident  extends user {

public Resident (int userID,String userName,String Password,int age,double money){
super(userID,userName,Password,age,money);
}

public   double payment( double fees ){
return fees*0.25;
}
}

// class Foreigner 
// --------------------------------
class Foreigner extends user {

public Foreigner (int userID,String userName,String Password,int age,double money){
super(userID,userName,Password,age , money);
}

public   double payment( double fees ){
return fees ;
}
}

// class router
// --------------------------
class router{
private int unique_serial_number ;
private String model ;
private int number_of_ports ;
private double price ;
public router(int serial_number , String model ,int number_of_ports ,double price  ){
  this.unique_serial_number=serial_number;
  this.price = price ;
  this.number_of_ports = number_of_ports ;
  this.model=model;  
}
public   String getmodel (){return model   ;}
public   int getnumber_of_ports(){return number_of_ports  ;}
public   int getunique_serial_number(){return unique_serial_number  ;}
public double getprice(){return price  ;}

}

// class reservation 
// --------------------------
class reservation {
 user   _user   ;
 router _router ;
 Date stdate ;
 Date enddate ;
 String type ;
 int days;
 public reservation (user _user, router _router,Date stdate,Date enddate,String type, int days) {
 this._user = _user ;
 this._router = _router ;
 this.stdate = stdate ;  
 this.enddate = enddate ; 
 this.type = type;
 this.days = days;
}
}
// class invoice 
// --------------------------
class invoice {
public invoice (String msg){
  JOptionPane.showMessageDialog(null, msg );
}
 

}
// InvadlidDataException
// -----------------------------------------
class InvadlidDataException extends Exception  {
  static int nEntries;
public InvadlidDataException  (String msg){
  JOptionPane.showMessageDialog(null, msg ,
      "Error", JOptionPane.ERROR_MESSAGE);
}

}


// Registerpanel 
// -----------------------------------------
class Registerpanel extends JPanel implements ActionListener   {
//  Employee employee[]=new Employee[3] ;

  
private int userID ;
private String userName ;
private String Password;
static int age ;

  JLabel lab1 = new JLabel("User ID");
  JLabel labAge = new JLabel("Age");
  JLabel lab2 = new JLabel("userName ");
  JLabel lab3 = new JLabel("Password");
  JLabel lab4 = new JLabel("Re-enter Password" );
  
  JTextField textField1=new JTextField();;
  JTextField textField2=new JTextField();;
  JTextField textField3=new JPasswordField ();;
  JTextField textField4=new JPasswordField ();;
  JTextField textFieldAge =new JTextField();;
 
 JButton  Registerbtn = new JButton("Register");
 
   public Registerpanel(){
      add(labAge); 
       add(textFieldAge); 
        add(lab1);
        add(lab2);
        add(lab3);
        add(lab4);
        add(textField1);
        add(textField2);
        add(textField3);
        add(textField4);

        add(Registerbtn );
      



  Registerbtn.setActionCommand("Register");
  Registerbtn.addActionListener(this);
  
} 
@Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);

        //setSize
        textField1.setSize(100,20);
         textField2.setSize(100,20);
          textField3.setSize(100,20);
         textField4.setSize(100,20);
        textFieldAge.setSize(100,20);
//pos
        
          lab1.setLocation(25,60);
         lab2.setLocation(25,80);
          lab3.setLocation(25,100);
         lab4.setLocation(25,120);
         labAge.setLocation(25,140);
          textField1.setLocation(200,60);
         textField2.setLocation(200,80);
          textField3.setLocation(200,100);
         textField4.setLocation(200,120);
textFieldAge.setLocation(200,140);

         
         Registerbtn.setLocation(150,220);
         
         

        
       
        

    }
 
void clear(){
  textField1.setText("");
         textField2.setText("");
          textField3.setText("");
         textField4.setText("");
         
}
   public void actionPerformed(ActionEvent e) {
 if ("Register".equals(e.getActionCommand())) {

Main.from1.remove(Main.pnl) ;
Main.pnl = new Loginpanel();
Main.from1.add(Main.pnl) ;
Main.from1.invalidate();
Main.from1.validate();
Main.from1.repaint();
    }  
}


}// end class

// Loginpanel 
// -----------------------------------------
class Loginpanel extends JPanel implements ActionListener   {


  

 JButton  Loginfbtn = new JButton("Login As Foreigner");
 JButton  Loginrbtn = new JButton("Login As Resident ");
   public Loginpanel(){
      
        
    
        add(Loginfbtn );
        add(Loginrbtn );
      




  Loginfbtn.setActionCommand("Loginf");
  Loginfbtn.addActionListener(this);

  Loginrbtn.setActionCommand("Loginr");
  Loginrbtn.addActionListener(this);
  
} 
@Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);

   
         Loginfbtn.setLocation(120,170);
         Loginrbtn.setLocation(120,200);
        
       
        

    }
 
 
   public void actionPerformed(ActionEvent e) {
     
   
 if ("Loginf".equals(e.getActionCommand())) {
   Main.allrouters=new ArrayList<router>();  
   Main.myrouters = new ArrayList<reservation>(); 
Main.allrouters();
Main.cur_user = Main.users.get(0);
Main.ch_panal(new homepanelwithlogin() );
    } else if ("Loginr".equals(e.getActionCommand())) {
 Main.allrouters=new ArrayList<router>();  
   Main.myrouters = new ArrayList<reservation>(); 
Main.allrouters();
Main.cur_user = Main.users.get(1);
Main.ch_panal(new homepanelwithlogin() );
    }
}


}// end class


// homepanelwithlogin 
// -----------------------------------------
class homepanelwithlogin  extends JPanel implements ActionListener   {
//  Employee employee[]=new Employee[3] ;
 
  JLabel lab2 = new JLabel("An Internet Router Rental System");
  JLabel lab3 = new JLabel("helps managing routers rental reservations");
   
  
  
   
   
  
 
 JButton  Newrouterbtn = new JButton("New router");
 JButton  myroutersbtn = new JButton("My routers");
 JButton  Logoutbtn = new JButton("Logout");
public homepanelwithlogin (){
      
        
        add(lab2);
        add(lab3);
         
        

     
    add( Newrouterbtn );
    add( myroutersbtn );
    add( Logoutbtn );
    

  Newrouterbtn.setActionCommand("Newrouter");
  Newrouterbtn.addActionListener(this);

  myroutersbtn.setActionCommand("myrouters");
  myroutersbtn.addActionListener(this);

  Logoutbtn.setActionCommand("Logout");
  Logoutbtn.addActionListener(this);
  
} 
@Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);

       
         
//pos
        
           
         lab2.setLocation(30,150);
          lab3.setLocation(30,200);
          
         

         
         Newrouterbtn.setLocation(25,20);
         myroutersbtn.setLocation(25,60);
         Logoutbtn.setLocation(300,20);
             
         

        
       
        

    }
 
 
   public void actionPerformed(ActionEvent e) {
     if ("Newrouter".equals(e.getActionCommand())) {
       if (Main.allrouters.size()!=0 )
    Main.ch_panal(new allroutersp( 0) );
    else
       JOptionPane.showMessageDialog(null,
         "there aren't new routers !");
    } 
    else if ("myrouters".equals(e.getActionCommand())) {
           if (Main.myrouters.size()!=0 )
    Main.ch_panal(new myroutersp( 0) );
    else
       JOptionPane.showMessageDialog(null,
         "you have no routers !");
    } else if ("Logout".equals(e.getActionCommand()))
    Main.ch_panal (new Loginpanel());
}


}// end class

// myrouters
// -----------------------------------------
class allroutersp  extends JPanel implements ActionListener   {
//  Employee employee[]=new Employee[3] ;
 

   
  int side;
  router active_router ;

  ButtonGroup group = new ButtonGroup();
  JRadioButton btn1 = new JRadioButton("daily");
  JRadioButton btn2 = new JRadioButton("weekly");JRadioButton btn3 = new JRadioButton("monthly");
  

  JTextField textField1=new JTextField("0");
   
  
  JLabel lab2 = new JLabel();
  JLabel lab3 = new JLabel();
  JLabel lab1 = new JLabel();
  JLabel lab4 = new JLabel();
  JLabel sidelab = new JLabel();
  JLabel datalab = new JLabel("days to start reservation");
 JButton  prevbtn = new JButton("prev ");
 JButton  nextbtn = new JButton("next");
 JButton  rentbtn = new JButton("rent ");
 
 JButton  Logoutbtn = new JButton("home");
public allroutersp (int side){
 
       this.side=Math.abs( side % Main.allrouters.size() );
       active_router = Main.allrouters.get(this.side);
      
      lab2.setText( "model   " + active_router.getmodel () );
     lab3.setText(   "ports   " + active_router.getnumber_of_ports() );
      lab1.setText(  "serial_number   " +active_router. getunique_serial_number() );
      lab4.setText(  "price  " +active_router.getprice());
      sidelab.setText(this.side+1 + " /  " +Main.allrouters.size() );
      
        group.add(btn1 );
        group.add(btn2 ); 
        group.add(btn3 ); 
        add(btn1);
        add(btn2);
        add(btn3);
        add(lab2);
        add(lab3);
        add(lab1);
        add(lab4);
        add(sidelab);
        add(datalab); 
        add(textField1);
     
    add( prevbtn );
    add( nextbtn );
    add( rentbtn );
    add( Logoutbtn );
    

  prevbtn.setActionCommand("prev");
  prevbtn.addActionListener(this);

  nextbtn.setActionCommand("next");
  nextbtn.addActionListener(this);

  rentbtn.setActionCommand("rent");
  rentbtn.addActionListener(this);

  Logoutbtn.setActionCommand("home");
  Logoutbtn.addActionListener(this);
  
} 
@Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);

       
         
//pos
        
           
        lab2.setLocation(150,50);
        lab3.setLocation(150,100);
        lab1.setLocation(150,150);
        lab4.setLocation(150,200);
        sidelab.setLocation(25,300);
        datalab.setLocation(50,22);
        textField1.setBounds(22,22,22,22);
        btn1.setLocation(100,250);
        btn2.setLocation(170,250);
        btn3.setLocation(240,250);
         
         rentbtn.setLocation(180,300);
         nextbtn.setLocation(300,180);
         prevbtn.setLocation(25,180);
         Logoutbtn.setLocation(300,20);
             
         

        
       
        

    }
 
 
   public void actionPerformed(ActionEvent e) {
    if ("next".equals(e.getActionCommand())) {
       Main.ch_panal(new allroutersp( this.side+1) );
    }  
    else if ("prev".equals(e.getActionCommand())) {
      if (this.side==0) this.side=Main.allrouters.size();
       Main.ch_panal(new allroutersp( this.side-1) );
    }  
    else if ("home".equals(e.getActionCommand())) {
       
       Main.ch_panal(new homepanelwithlogin()  );
    } 
    else if ("rent".equals(e.getActionCommand())) {
      String type; int days;
       if(btn1.isSelected()){ type="daily" ;days=1; }
     else if(btn2.isSelected()) {type ="weekly" ; days=7;}
     else if (btn3.isSelected()) {type = "monthly" ;days=30;}
     else {
        JOptionPane.showMessageDialog(null,
         "Select daily , weekly or monthly " ,
      "Error", JOptionPane.ERROR_MESSAGE); return ;
     }
     if ( Main.cur_user.payment(this.active_router.getprice() * days ) > Main.cur_user.getMoney()  ){
       JOptionPane.showMessageDialog(null,
         " you need   " + Main.cur_user.payment(this.active_router.getprice() * days ),
      "Error", JOptionPane.ERROR_MESSAGE); return ;
     }
    //   msg what you will give money
 
    if(JOptionPane.showConfirmDialog(null, "you will pay "+ Main.cur_user.payment(this.active_router.getprice() * days ), "alert", JOptionPane.OK_CANCEL_OPTION)==0){
    Date now =Calendar.getInstance().getTime();
    now.setHours(now.getHours()+ (int)Integer.parseInt( textField1.getText() )*24);
     Date st=now;
     now =Calendar.getInstance().getTime();
    now.setHours(now.getHours()+ days*24);
   Main.myrouters.add(
      new reservation(Main.cur_user , this.active_router
      , st, now ,type,days
      )
     );
     Main.cur_user.setmoney(Main.cur_user.getMoney()-Main.cur_user.payment(this.active_router.getprice() * days ));
     // remove router form  allrouters
     Main.allrouters.remove(this.side);
       JOptionPane.showMessageDialog(null,
         " done ! \nserial_number  "+ active_router.getunique_serial_number() +" \nreservation number "+Main.myrouters.size()+"\nfees "+Main.cur_user.payment(this.active_router.getprice() * days ) );
    
      if (Main.allrouters.size()!=0 )
    Main.ch_panal(new allroutersp( this.side) );
    else
       { Main.ch_panal(new homepanelwithlogin());}
   

    }

   
    }          
}


}// end class


// myrouters
// -----------------------------------------
class myroutersp  extends JPanel implements ActionListener   {
//  Employee employee[]=new Employee[3] ;
 

   
  int side;
  router active_router ;
 reservation active_Reservation ;
   
  JLabel lab2 = new JLabel();
  JLabel lab3 = new JLabel();
  JLabel lab1 = new JLabel();
  JLabel lab4 = new JLabel();
  JLabel sidelab = new JLabel();
 JButton  prevbtn = new JButton("prev ");
 JButton  nextbtn = new JButton("next");
 JButton  extendbtn = new JButton("extend ");
 JButton  cancelbtn = new JButton("cancel ");
 JButton  Logoutbtn = new JButton("home");
public myroutersp (int side){
  
       this.side=Math.abs( side % Main.myrouters.size() );
        active_Reservation = Main.myrouters.get(this.side);
       active_router = active_Reservation._router;
      
      lab2.setText( "model   " + active_router.getmodel () );
     lab3.setText(   "endDate   " + active_Reservation.enddate );
     
      lab1.setText(  "type   " + active_Reservation.type) ;
      lab4.setText(  "start data  " +active_Reservation.stdate);
      sidelab.setText(this.side+1 + " /  " +Main.myrouters.size() );
      
      
        add(lab2);
        add(lab3);
        add(lab1);
        add(lab4);
        add(sidelab);

     
    add( prevbtn );
    add( nextbtn );
    add( cancelbtn );
    add( extendbtn );
    add( Logoutbtn );
    

  prevbtn.setActionCommand("prev");
  prevbtn.addActionListener(this);

  nextbtn.setActionCommand("next");
  nextbtn.addActionListener(this);

  extendbtn.setActionCommand("extend");
  extendbtn.addActionListener(this);

  cancelbtn.setActionCommand("cancel");
  cancelbtn.addActionListener(this);

  Logoutbtn.setActionCommand("home");
  Logoutbtn.addActionListener(this);
  
} 
@Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);

       
         
//pos
        
           
        lab2.setLocation(150,50);
        lab3.setLocation(50,100);
        lab1.setLocation(150,150);
        lab4.setLocation(50,220);
        sidelab.setLocation(25,300);

        
       
        cancelbtn.setLocation(130,300);
        extendbtn.setLocation(230,300);
        nextbtn.setLocation(300,180);
        prevbtn.setLocation(25,180);
        Logoutbtn.setLocation(300,20);
             
         

        
       
        

    }
 
 
   public void actionPerformed(ActionEvent e) {
    if ("next".equals(e.getActionCommand())) {
       Main.ch_panal(new myroutersp( this.side+1) );
    }  
    else if ("prev".equals(e.getActionCommand())) {
      if (this.side==0) this.side=Main.myrouters.size();
       Main.ch_panal(new myroutersp( this.side-1) );
    }  
    else if ("home".equals(e.getActionCommand())) {
     Main.ch_panal(new homepanelwithlogin()  );
    }
    else if ("extend".equals(e.getActionCommand())) {
  if(JOptionPane.showConfirmDialog(null, "you will pay "+ Main.cur_user.payment(this.active_router.getprice() * active_Reservation.days ), "alert", JOptionPane.OK_CANCEL_OPTION)==0)
   { active_Reservation.enddate.setHours(active_Reservation.enddate.getHours()+ active_Reservation.days*24);

     Main.cur_user.setmoney(Main.cur_user.getMoney()-Main.cur_user.payment(this.active_router.getprice() * active_Reservation.days ));

  
       JOptionPane.showMessageDialog(null,
         " done ! " );
     Main.ch_panal(new myroutersp(this.side));    
   }
    }
    else if ("cancel".equals(e.getActionCommand())) {
       
         
    long diff =  active_Reservation.stdate.getTime() - Calendar.getInstance().getTime().getTime();
    diff=diff / 1000 / 60 / 60 / 24;
    if(diff<2){
  JOptionPane.showMessageDialog(null,
         "you can't cancel " ,
      "Error", JOptionPane.ERROR_MESSAGE);
      return;
    }
    Main.cur_user.setmoney(Main.cur_user.payment(this.active_router.getprice() * active_Reservation.days ));
     Main.allrouters.add(active_router);
     Main.myrouters.remove(this.side);
    
     if( Main.myrouters.size()!=0)
      Main.ch_panal(new myroutersp(this.side)); 
     else
      Main.ch_panal(new homepanelwithlogin()); 
    }          
}


}// end class

// Main
// -----------------------------------------
class Main {
// cur_user
// User data
// chage panal()

public static ArrayList<user> users = new ArrayList<user>();
public static ArrayList <router> allrouters = new ArrayList<router>();  
  public static ArrayList <reservation> myrouters = new ArrayList<reservation>(); 
 public static user cur_user;
  public static JPanel  pnl ;
  public static JFrame from1= new JFrame();
  public static void ch_panal(JPanel newJPanel ){
    from1.remove(pnl) ;
    pnl = newJPanel;
    from1.add(pnl) ;
    from1.invalidate();
    from1.validate();
    from1.repaint();
  }
  public static void allrouters(){
   router _rouuter=new router(000,"xxx",3000,10);
   allrouters.add(_rouuter);
   _rouuter=new router(001,"xxo",3200,20);
   allrouters.add(_rouuter);
   _rouuter=new router(002,"xxu",3100,12);
   allrouters.add(_rouuter);
  }
  public static void allusers(){
   user _user=new Foreigner(0, "test1", "0000", 20,3000) ;
   users.add(_user);
   _user=new Resident(1, "test2", "2222", 22 , 2000) ;
     users.add(_user);
  }  
  public static void main(String[] args) {
    // System.out.println("Hello world!");
    allusers();
    allrouters();
    pnl= new Loginpanel();
   SwingUtilities.updateComponentTreeUI(from1);
   from1.add(pnl);
   from1.setSize(400, 400);

    from1.setVisible(true);
    

  }
}
