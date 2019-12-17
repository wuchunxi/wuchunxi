# wuchunxi
package loginform;

import registerform.LoginSucceed;
import utils.Tool;
import utils.ToolManger;

import javax.swing.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

/**
 * @program: classprogram
 * @Description:登陆界面，通过监听登录按钮跳到管理界面，其中登录文件信息保存在information.txt文件，管理信息保存在mangerinformation.txt。
 * @author: wcx
 * @date: 2019-12-17
 */
public class LoginForm extends JFrame {

    private JPanel panelLogin;
    private JLabel userLabel;
    private JTextField userText;
    private JLabel passwordLabel;
    private JPasswordField passwordText;
    private JButton loginButton;
    private JButton registerButton;

    public JButton getRegisterButton() {
        return registerButton;
    }

    public LoginForm(){
        setTitle("Login Form");
        setSize(280, 160);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        panelLogin = new JPanel();
        panelLogin.setLayout(null);

        userLabel = new JLabel("User:");
        userLabel.setBounds(10,20,80,25);
        panelLogin.add(userLabel);

        userText = new JTextField(20);
        userText.setBounds(100,20,165,25);
        panelLogin.add(userText);

        passwordLabel = new JLabel("Password:");
        passwordLabel.setBounds(10,50,80,25);
        panelLogin.add(passwordLabel);

        passwordText = new JPasswordField(20);
        passwordText.setBounds(100,50,165,25);
        panelLogin.add(passwordText);

        loginButton = new JButton("login");
        loginButton.setBounds(10, 100, 80, 25);
        panelLogin.add(loginButton);
        loginButton.addActionListener(new LoginEventListen());

        registerButton = new JButton("register");
        registerButton.setBounds(100, 100, 80, 25);
        panelLogin.add(registerButton);

        add(panelLogin);


    }


    class LoginEventListen implements ActionListener{

        @Override
        public void actionPerformed(ActionEvent e) {
            ToolManger toolManger = new ToolManger();
            Tool tool = new Tool();
            String Manger = userText.getText();
            String mpassword =String.valueOf( passwordText.getPassword());
            String User = userText.getText();
            String password =String.valueOf( passwordText.getPassword());
            if(tool.loginForm(User,password)==1 ){
                LoginSucceed loginSucceed = new LoginSucceed();
                loginSucceed.setFrameLoginSucceedVisible(true);
                dispose();
            }
            if(toolManger.mangerForm(Manger,mpassword )==1 ){
                MangerForm  mangerForm = new MangerForm();
                mangerForm.setFrameMangerFormVisible(true);
            }

        }
    }

    /**
     * @Description: 设置界面可见
     * @Param: [visible]
     * @return: void
     * @Author: wcx
     * @Date: 2019-12-17
     */
    public void setFrameLoginVisible(Boolean visible){
    setVisible(visible);
}
}
管理界面
package loginform;

import utils.ToolManger;

import javax.swing.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

/**
 * @author :wcx
 * @DATE:2019-12-17
 * @Description:管理员界面，通过监听修改按钮跳到密码修改成功界面
 */
public class MangerForm extends JFrame {
    final String COMMAND_MODIFY = "MODIFY";
    private JPanel panelManger;
    private JLabel mangerLabel;
    private JTextField userText;
    private JLabel mangerPasswordLabel;
    private JPasswordField passwordText;
    private JButton quitButton;
    private JButton modifyButton;
    public MangerForm() {
        setTitle("Manger Succeed");
        setSize(280, 160);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        JPanel panelLoginSucceed = new JPanel();
        panelLoginSucceed.setLayout(null);

        panelManger  = new JPanel();
        panelManger .setLayout(null);

        mangerLabel = new JLabel("Manger:");
        mangerLabel.setBounds(10, 20, 80, 25);
        panelManger.add(mangerLabel);

        userText = new JTextField(20);
        userText.setBounds(100, 20, 165, 25);
        panelManger.add(userText);

        mangerPasswordLabel = new JLabel("MangerPassword:");
        mangerPasswordLabel.setBounds(10, 50, 80, 25);
        panelManger.add(mangerPasswordLabel);

        passwordText = new JPasswordField(20);
        passwordText.setBounds(100, 50, 165, 25);
        panelManger.add(passwordText);

        quitButton = new JButton("Quit");
        quitButton.setBounds(100, 100, 80, 25);
        panelManger.add(quitButton);


        modifyButton = new JButton("Modify");
        modifyButton.setBounds(10, 100, 80, 25);
        panelManger.add(modifyButton);
        modifyButton.setActionCommand(COMMAND_MODIFY);

        add(panelManger);
        ActionListener mangerActionListener = new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String command = e.getActionCommand();
                if(COMMAND_MODIFY.equals(command)){
                    PasswordModifySucceed passwordModifySucceed = new PasswordModifySucceed();
                    passwordModifySucceed.setFrameModifySucceed(true);
                }
            }
        };
        modifyButton.addActionListener(mangerActionListener);
    }



    public void setFrameMangerFormVisible(Boolean visible){
        setVisible(visible);
    }

}
登录成功界面：
package registerform;

import javax.swing.*;

/**
 * @author wcx
 */
public class LoginSucceed extends JFrame  {
    public LoginSucceed() {
        setTitle("Login Succeed");
        setSize(280, 160);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        JPanel panelLoginSucceed = new JPanel();
        panelLoginSucceed.setLayout(null);

    }

    public void setFrameLoginSucceedVisible(Boolean visible){
        setVisible(visible);
    }
}
修改密码成功界面：
package loginform;

import javax.swing.*;

/**
 * @author wcx
 * @ATE:2019-12-17
 */
public class PasswordModifySucceed extends JFrame  {
    public PasswordModifySucceed () {
        setTitle("modify Succeed");
        setSize(280, 160);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        JPanel modifySucceed = new JPanel();
        modifySucceed.setLayout(null);

    }

    public void setFrameModifySucceed(Boolean visible){
        setVisible(visible);
    }
}
检测登录信息是否匹配：
package utils;

import java.io.*;

/**
 * @author wcx
 * @DATE:2019-12-17
 * @Description:此段程序命名错误，应为ToolLogin,检测登录信息是否匹配
 */
public class ToolRegister2 {
    public int registerForm(String User, String password) {
        int result = 0;
        String filename = "information.txt";
        File file = new File(filename);
        if (file.exists()) {
            /*读用户信息*/
            try {
                BufferedReader loginBufferedReader = new BufferedReader(new FileReader(file));
                String username = loginBufferedReader.readLine();
                String userpassword = loginBufferedReader.readLine();
                loginBufferedReader.close();
                if (username.equals(User) && userpassword.equals(password)) {
                    result = 1;
                }
            } catch (FileNotFoundException e) {
                e.printStackTrace();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
        return result;
    }
}

检测管理信息是否匹配：
package utils;
import java.io.*;
/**
 * @author wcx
 * @DATE:2019-12-17
 * @DESCRIPTION:检测管理信息是否匹配
 */
public class ToolManger {


    public int mangerForm(String Manger, String mpassword) {
        int result = 0;
        String filename = "mangerinformation.txt";
        File file = new File(filename);
        if (file.exists()) {
            /*读用户信息*/
            try {
                BufferedReader mangerBufferedReader = new BufferedReader(new FileReader(file));
                String mangername = mangerBufferedReader.readLine();
                String mangerpassword = mangerBufferedReader.readLine();
                mangerBufferedReader.close();
                if (mangername.equals(Manger) && mangerpassword.equals(mpassword)) {
                    result = 1;
                }
            } catch (FileNotFoundException e) {
                e.printStackTrace();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
        return result;
    }
}
主函数：
import loginform.LoginForm;


/**
 * @program: classprogram
 * @Description:
 * @author: wcx
 * @date: 2019-12-17
 */
public class Manage {
    public static void main(String[] args){
        LoginForm loginForm = new LoginForm();
        loginForm.setFrameLoginVisible(true);

    }
}
