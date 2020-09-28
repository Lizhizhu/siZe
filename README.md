import java.awt.BorderLayout;
import java.awt.Color;
import java.awt.Font;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JMenu;
import javax.swing.JMenuBar;
import javax.swing.JMenuItem;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JTextField;
public class B extends JFrame implements ActionListener{     //界面的设计
    int max=20;
    int MAX=10;   
    int TYPE=1;
    JLabel jlTitle=new JLabel();            
    JLabel jl=new JLabel("");
    JLabel jlAnswer=new JLabel("");
    JLabel jlTotal=new JLabel("共"+max+"题");        
    JLabel jlcorrect=new JLabel();
    JTextField jtf=new JTextField(3);
    JMenuBar jmb=new JMenuBar();
    JMenu jm=new JMenu("类型 ");                                //建立一个可选菜单
    JMenuItem jmi1=new JMenuItem("10以内加法");
    JMenuItem jmi2=new JMenuItem("10以内减法");
    JMenuItem jmi3=new JMenuItem("20以内加法");
    JMenuItem jmi4=new JMenuItem("20以内减法");
    JMenuItem jmi5=new JMenuItem("100以内加法");
    JMenuItem jmi6=new JMenuItem("100以内减法");
    JMenuItem jmi7=new JMenuItem("100以内乘法");
    JMenuItem jmi8=new JMenuItem("100以内除法");
    JMenuItem jmi9=new JMenuItem("真分数的计算");    
    JButton jb1=new JButton("上一题");
    JButton jb2=new JButton("下一题");           //创建button
    JButton jb3=new JButton("评卷");
    JButton jb4=new JButton("答案");
    JPanel jp1=new JPanel();
    JPanel jp2=new JPanel();
    JPanel jp3=new JPanel();
    String[] question=new String[max];       //利用字符串列表来存储问题
    int[] answer=new int[max];
    String[] studentAnswer=new String[max];   //利用字符串列表来存储答案
    boolean[]correct=new boolean[max];
    int count=1;
    boolean submitFlag=false;
    B(){
        super("小学数学测试"); 
        jlTitle.setFont(new Font(null,Font.PLAIN,20));
        jlTotal.setFont(new Font(null,Font.PLAIN,20));      ///字体的设置
        jlAnswer.setFont(new Font(null,Font.PLAIN,20));
        jl.setFont(new Font(null,Font.PLAIN,20));
        jlcorrect.setFont(new Font(null,Font.PLAIN,20));
        jlcorrect.setForeground(Color.RED);
        jtf.setFont(new Font(null,Font.PLAIN,20));
        fillQuestion();
        jb1.addActionListener(this);
        jb2.addActionListener(this);
        jb3.addActionListener(this);
        jb4.addActionListener(this);
        jmi1.addActionListener(this);
        jmi2.addActionListener(this);
        jmi3.addActionListener(this);
        jmi4.addActionListener(this);        
        jmi5.addActionListener(this);
        jmi6.addActionListener(this);
        jmi7.addActionListener(this);
        jmi8.addActionListener(this);                           // 菜单栏的添加
        jm.add(jmi1);jm.add(jmi2);jm.add(jmi3);jm.add(jmi4);jm.add(jmi5);jm.add(jmi6);jm.add(jmi7);jm.add(jmi8);
        jmb.add(jm);
        setJMenuBar(jmb);
        jp1.add(jlTitle);jp1.add(jlTotal);jp1.add(jb3);jp1.add(jb4);
        jp2.add(jl);jp2.add(jtf);jp2.add(jlcorrect);jp2.add(jlAnswer);    //利用panel实现多条文档显示输出
        jp3.add(jb1);jp3.add(jb2);
        add(jp1,BorderLayout.NORTH);
        add(jp2,BorderLayout.CENTER);
        add(jp3,BorderLayout.SOUTH);
        setSize(300, 200);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);  //使用完解放退出
        setLocationRelativeTo(null);
        setVisible(true);               ///窗口可视化
    }
    @Override
    public void actionPerformed(ActionEvent ae) {
        if(ae.getSource()==jb1){
        if(submitFlag==false){
            try{        //点击上一题时抓取用户的不正常输入
            float tempanswer=Integer.valueOf(jtf.getText().trim());  //去除掉多余的空格
            studentAnswer[count-1]=jtf.getText().trim();
            if(count==1)
                count=max;
            else count--;
            jlTitle.setText("第"+count+"题");
            jl.setText(question[count-1]);
            jtf.setText("");
            if(studentAnswer[count-1]==null||studentAnswer[count-1].equals(""))
            {        ///若是出现空白输入，则提醒用户
            }
            else
            {
                jtf.setText(studentAnswer[count-1]);
            }
            }catch(Exception nfe){
                JOptionPane.showMessageDialog(this, "请输入正整数!");
                jtf.requestFocus();
                }
            }
            else{
                if(count==1)count=max;
                else count--;
                jlTitle.setText("第"+count+"题");    
                jl.setText(question[count-1]);
                jlAnswer.setText("");
                jtf.setEnabled(false);
                jtf.setText(studentAnswer[count-1]);
                jb4.setEnabled(true);
                if(correct[count-1]==true){
                    jlcorrect.setText("√");                        // 显示答案正确与否
                }
                else{
                    jlcorrect.setText("×");
                }
            }
        }        
        if(ae.getSource()==jb2){
            if(submitFlag==false){
                try{                                                      //点击下一题时抓取用户的不正常输入
                    float tempanswer=Integer.valueOf(jtf.getText().trim());    
                    studentAnswer[count-1]=jtf.getText().trim();
                    if(count==max)count=1;
                    else count++;
                    jlTitle.setText("第"+count+"题");
                    jl.setText(question[count-1]);
                    jtf.setText("");
                    if(studentAnswer[count-1]==null||studentAnswer[count-1].equals(""))
                    {
                    }
                    else
                    {
                        jtf.setText(studentAnswer[count-1]);
                    }
                }
                catch(Exception nfe)
                {
                    JOptionPane.showMessageDialog(this, "请输入正整数!");
                    jtf.requestFocus();
                }    
            }
            else
            {
                if(count==max)count=1;
                else count++;
                jlTitle.setText("第"+count+"题");
                jl.setText(question[count-1]);
                jlAnswer.setText("");
                jtf.setEnabled(false);
                jtf.setText(studentAnswer[count-1]);
                jb4.setEnabled(true);
                if(correct[count-1]==true){
                    jlcorrect.setText("√");
                }
                else{
                    jlcorrect.setText("×");
                }
            }    
        }
        if(ae.getSource()==jb3){
            try{                                                                    //点击评卷时检测用户的不正常输入，并给出全卷情况
                float tempanswer=Integer.valueOf(jtf.getText().trim());
                studentAnswer[count-1]=jtf.getText().trim();
                for(int i=0;i<max;i++){
                    if(studentAnswer[i]==null||studentAnswer[i].equals("")){
                        correct[i]=false;
                    }
                    else if(Float.valueOf(studentAnswer[i])==answer[i]){
                        correct[i]=true;
                    }
                    else{
                        correct[i]=false;
                    }
                }
                int correctAnswer=0;
                for(int i=0;i<max;i++){
                    if(correct[i]==true){
                        correctAnswer++;
                    }
                }
                String s="共"+max+"道题\n";
                s=s+"答对"+correctAnswer+"道题\n";
                s=s+"答错"+(max-correctAnswer)+"道题\n";
                s=s+"成绩"+String.format("%.2f",(100*(float)correctAnswer/max))+"分\n";
                JOptionPane.showMessageDialog(this, s);
                submitFlag=true;
                jb4.setEnabled(true);
                jtf.setEnabled(false);
                jtf.setText(studentAnswer[count-1]);
                if(correct[count-1]==true){
                    jlcorrect.setText("√");
                }
                else{
                    jlcorrect.setText("×");
                }
            }
            catch(Exception nfe){
                JOptionPane.showMessageDialog(this, "请输入正整数!");
                jtf.requestFocus();
            }
        }
        if(ae.getSource()==jb4){
            jlAnswer.setText(String.valueOf(answer[count-1]));
        }
        if(ae.getSource()==jmi1){
            MAX=10;TYPE=1;fillQuestion();       //菜单的选项
        }
        if(ae.getSource()==jmi2){
            MAX=10;TYPE=2;fillQuestion();
        }
        if(ae.getSource()==jmi3){
            MAX=20;TYPE=1;fillQuestion();
        }
        if(ae.getSource()==jmi4){
            MAX=20;TYPE=2;fillQuestion();
        }
        if(ae.getSource()==jmi5){
            MAX=100;TYPE=1;fillQuestion();
        }
        if(ae.getSource()==jmi6){
            MAX=100;TYPE=2;fillQuestion();
        }
        if(ae.getSource()==jmi7){
            MAX=100;TYPE=3;fillQuestion();
        }
        if(ae.getSource()==jmi8){
            MAX=100;TYPE=4;fillQuestion();
        }
    }    
    public static void main(String[] args) {
        new B();
    }
    public void fillQuestion(){
        count=1;
        for(int i=0;i<max;i++){
        String s=randomQuestion(MAX,TYPE);                 //问题的随机放出
        question[i]=s.substring(0,s.indexOf("=")+1);
        answer[i]=Integer.valueOf(s.substring(s.indexOf("=")+1));
    }
    studentAnswer=new String[max];
    correct=new boolean[max];
    jl.setText(question[0]);
    jlTitle.setText("第"+count+"题");
    jlcorrect.setText("");
    jlAnswer.setText("");
    submitFlag=false;
    jtf.setEnabled(true);
    jtf.setText("");
    jb4.setEnabled(false);
    }
    public String randomQuestion(int MAX,int TYPE) {
        String s="";
        int answer=MAX+1;
        while(answer>MAX||answer<0){   ///random随机出正整数
            int a=(int)(Math.random()*MAX+1);
            int b=(int)(Math.random()*MAX+1);
            int c=(int)(Math.random()*MAX+1);
            int d=(int)(Math.random()*MAX+1);
            switch(TYPE){
                case 1:answer=a+b;break;
                case 2:answer=a-b;break;
                case 3:answer=a*b;break;
                case 4:
                if(a%b==0){
                    answer=a/b;
                }
                break;
            }
            if(answer<=MAX&&answer>=0){
                s=s+a;
                switch(TYPE){
                    case 1:s=s+"+";break;
                    case 2:s=s+"-";break;
                    case 3:s=s+"*";break;
                    case 4:s=s+"/";break;
                }    
                s=s+b+"="+answer;
            }
        }
        return s;
    }
}
