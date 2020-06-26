
import javax.swing.JFrame;

import java.awt.Graphics;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.*;


 class Employee{
private int EmpID ;
private String EmpName ;
private String Password;
static int nEmployees ;
public Employee(){
 
}
public   void setEmpID (int EmpID ){this.EmpID=EmpID ;}
public   void setEmpName (String EmpName ){this.EmpName=EmpName ;}
public   void setPassword(String Password){this.Password=Password ;}
public   int getEmpID(){ return EmpID ; }
public   String getEmpName (){return EmpName   ;}
public   String getPassword(){return Password  ;}
}



// clas PermanantEmp 
// --------------------------------
class PermanantEmp extends Employee {
private double BonusRate;
public PermanantEmp (){
 BonusRate=0.1;
}
public   void setBonusRate(double  BonusRate){this.BonusRate=BonusRate;}
public   double getBonusRate(){ return BonusRate; }
}


// Manager  class
// --------------------------------
class Manager extends PermanantEmp {
private static  int NumberOfEmployeesManged;

 public  Manager (){
 NumberOfEmployeesManged++;
}
public static  void setBonusRate(int  NumberOfEmployees){ NumberOfEmployeesManged=NumberOfEmployees;}
public   int getNumberOfEmployeesManged(){ return NumberOfEmployeesManged; }
}


// TempEmp class
// --------------------------------
class TempEmp extends Employee{
private float HourlyRate ;
public TempEmp (){
 HourlyRate=150f;
}
public   void setHourlyRate(float HourlyRate){this.HourlyRate= HourlyRate ;}
public   float getHourlyRate(){ return HourlyRate;}
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

// panel
// -----------------------------------------
class panel extends JPanel implements ActionListener   {
 Employee employee[]=new Employee[3] ;
  ButtonGroup group = new ButtonGroup();
  JRadioButton btn1 = new JRadioButton("Manager");
  JRadioButton btn2 = new JRadioButton("Permanant Employee"); 
  JRadioButton btn3 = new JRadioButton("Temp Employee");
  
  JLabel lab1 = new JLabel("Emplyee ID"); 
  JLabel lab2 = new JLabel("Employ Name");
  JLabel lab3 = new JLabel("Employee Password");
  JLabel lab4 = new JLabel("Re-enter Employee Password" );
  JTextField textField1=new JTextField();;
  JTextField textField2=new JTextField();;
  JTextField textField3=new JPasswordField ();;
  JTextField textField4=new JPasswordField ();;
  JButton  b1 = new JButton("Add Employee");
 JButton  b2 = new JButton("Display Extra Attribute");
   public panel(){
      group.add(btn1 );
        group.add(btn2 ); 
      group.add(btn3 ); 
        add(btn1);
        add(btn2);
        add(btn3);
        add(lab1);
        add(lab2);
        add(lab3);
        add(lab4);
        add(textField1);
        add(textField2);
        add(textField3);
        add(textField4);

        add(b1);
        add(b2);



  b1.setActionCommand("add");
  b1.addActionListener(this);
  b2.setActionCommand("display");
  b2.addActionListener(this);
} 
@Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);

        //setSize
        textField1.setSize(100,20);
         textField2.setSize(100,20);
          textField3.setSize(100,20);
         textField4.setSize(100,20);
//pos
        
          lab1.setLocation(25,60);
         lab2.setLocation(25,80);
          lab3.setLocation(25,100);
         lab4.setLocation(25,120);
          textField1.setLocation(300,60);
         textField2.setLocation(300,80);
          textField3.setLocation(300,100);
         textField4.setLocation(300,120);
         btn1.setLocation(200,150);
         btn2.setLocation(200,170);
         btn3.setLocation(200,190);
         b1.setLocation(150,220);
         b2.setLocation(120,250);
         

        
       
        

    }
void setEmp(Employee emp){
  try{
 emp.setEmpID ( (int) Integer.parseInt(textField1.getText()) );
              emp.setEmpName ( textField2.getText());
              emp.setPassword(textField3.getText()) ;
  }catch(Exception  e){

  }
            
}
void clear(){
  textField1.setText("");
         textField2.setText("");
          textField3.setText("");
         textField4.setText("");
         group.clearSelection();
}
   public void actionPerformed(ActionEvent e) {
 if ("add".equals(e.getActionCommand())) {
if(Employee.nEmployees==3){
new InvadlidDataException("Maximum Number of Invalid data entries reached, try anagin later") ;
b1.setEnabled(false);
return;
}
if(!(textField3.getText().equals(textField4.getText()))){
new InvadlidDataException("The password you entered the second time does not match the first time") ;
return;
}
     if(btn1.isSelected()){
employee[Employee.nEmployees++]=new Manager();
  setEmp(employee[Employee.nEmployees-1]); 
         clear();
         JOptionPane.showMessageDialog(null,"now manager added" );
}
     else if(btn2.isSelected()){
      employee[Employee.nEmployees++]=new PermanantEmp();
      setEmp(employee[Employee.nEmployees-1]);      
      clear();
        JOptionPane.showMessageDialog(null,"now Permanant Emp added" );
}
     else if (btn3.isSelected()){
       employee[Employee.nEmployees++]=new TempEmp();
       setEmp(employee[Employee.nEmployees-1]); 
       clear();
         JOptionPane.showMessageDialog(null,"now Temp Emp added" );
}
     else{ new InvadlidDataException("Must Select Employee type") ;}

   
    } else if ("display".equals(e.getActionCommand())) {
         if(employee[Employee.nEmployees-1] instanceof Manager) 
         JOptionPane.showMessageDialog(null, "Number Of Employees Manged   " + ((Manager) employee[Employee.nEmployees-1]).getNumberOfEmployeesManged() );
         else if(employee[Employee.nEmployees-1] instanceof PermanantEmp) JOptionPane.showMessageDialog(null, "Bonus Rate  " + ((PermanantEmp) employee[Employee.nEmployees-1]).getBonusRate());
         else if(employee[Employee.nEmployees-1] instanceof TempEmp)JOptionPane.showMessageDialog(null, "Hourly Rate " + ((TempEmp) employee[Employee.nEmployees-1]).getHourlyRate());

    }
}


}

// Main
// -----------------------------------------
class Main {
  public static void main(String[] args) {
    // System.out.println("Hello world!");
   JFrame from1= new JFrame();
   from1.add(new panel());
   from1.setSize(400, 400);

    from1.setVisible(true);
    

  }
}
