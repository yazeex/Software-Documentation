# Online Banking System User Manual

## Introduction
The TMT Banking System is a straightforward, user-friendly software designed to facilitate
basic banking operations. It aims to enhance customers’ experience by offering
essential financial services efficiently and securely. With intuitive navigation and a focus
on simplicity, the TMT system provides access to fundamental banking functionalities
while maintaining data security and convenience

## System Architecture
The TMT Banking System is designed as a client-server architecture, facilitating online banking operations. It is divided into multiple layers, ensuring scalability, security, and performance. Here’s a breakdown of the system architecture:

### Main Components

1. **Login and Registration**: Allows customers to create new accounts and access
existing ones securely.

3. **Transfers**: Supports intra-system fund transfers for seamless transactions.

5. **Deposit and Withdrawal**: Users can manage their finances by depositing or
withdrawing funds conveniently.
 
7. **View Balance**: Offers real-time updates on account balances.
 
9. **Change PIN**: change Personal Identification Numbers
(PIN) to ensure security.

11. **Profile edit**: Displays a customer list with essential details such as
name, account type, and contact information.



### System Flow Example: Login Process
1. **Client Layer**: The user inputs their account number and PIN on the login screen.

2. **Application Layer**: The credentials are sent to the application layer, where they are verified against the database.

3. **Data Access Layer**:A query is executed to match the credentials with the stored user data in the database.

4. **Application Layer**: If valid, a session is initiated for the user, and they are granted access. If invalid, an error message is returned.

5. **Client Layer**:The result (success or error) is displayed to the user.



---


## Core Components and Modules

### 1.**Login**
- **Purpose**:Authenticates a user by checking their account number and PIN.

  #### Key Methods:
  ```java
  private void LogonActionPerformed(java.awt.event.ActionEvent evt) {
    String sql = "select * from Account where Acc=? and Pin=?";
    try {
        pst = conn.prepareStatement(sql);
        pst.setString(1, AccnumLP.getText());
        pst.setString(2, PinLP.getText());
        rs = pst.executeQuery();
        if (rs.next()) {
            setVisible(false);
            Loading ob = new Loading();
            ob.setUpLoading();
            ob.setVisible(true);
            rs.close();
            pst.close();
        } else {
            JOptionPane.showMessageDialog(null, "Incorrect login");
        }
    } catch (Exception e) {
        JOptionPane.showMessageDialog(null, e);
    }
  }

### 2.**Registration**
- **Purpose**:Creates a new account by registering a user with the required details

  #### Key Methods:
```java
private void CreateActionPerformed(java.awt.event.ActionEvent evt) {
    String sql = "insert into Account(Acc,Name,DOB,Pin,Acc_Type,Ethnicity,MICR_No,Gender,Mob,Address,Sec_Q,Sec_A,Balance) values (?,?,?,?,?,?,?,?,?,?,?,?,?)";
    try {
        pst = conn.prepareStatement(sql);
        pst.setString(1, AccnumAP.getText());
        pst.setString(2, FullnameAP.getText());
        pst.setString(3, ((JTextField)DateofbirthAP.getDateEditor().getUiComponent()).getText());
        pst.setString(4, PinAP.getText());
        pst.setString(5, (String) AcctypeAP.getSelectedItem());
        pst.setString(6, (String) EthnicityAP.getSelectedItem());
        pst.setString(7, MnumAP.getText());
        pst.setString(8, buttonGroup1.getSelection().getActionCommand());
        pst.setString(9, MobileAP.getText());
        pst.setString(10, AddressAP.getText());
        pst.setString(11, (String) SecurityqAP.getSelectedItem());
        pst.setString(12, AnswerAP.getText());
        pst.setString(13, AmountxtAP.getText());
        pst.execute();
        JOptionPane.showMessageDialog(null, "Success! Account has been created");
        Bal();
    } catch (Exception e) {
        JOptionPane.showMessageDialog(null, e);
    }
}
```
### 3.**Transfers**
- **Purpose**:Transfers a specified amount between accounts.

    #### Key Methods:
```java
private void TransferActionPerformed(java.awt.event.ActionEvent evt) {
    String sql = "update Account set Balance=? where Acc=?";
    try {
        pst = conn.prepareStatement(sql);
        pst.setString(1, NewbalTransfer.getText());
        pst.setString(2, AccnumTransfer.getText());
        pst.executeUpdate();
        JOptionPane.showMessageDialog(null, "Transfer Successful");
    } catch (Exception e) {
        JOptionPane.showMessageDialog(null, e);
    }
}
```
### 3.**Deposit**
- **Purpose**:Deposits a specified amount into the user's account.

    #### Key Methods:
```java
private void DepositActionPerformed(java.awt.event.ActionEvent evt) {
    String sql = "update Account set Balance=? where Acc=?";
    try {
        pst = conn.prepareStatement(sql);
        pst.setString(1, NewbalDeposit.getText());
        pst.setString(2, AccnumDeposit.getText());
        pst.executeUpdate();
        JOptionPane.showMessageDialog(null, "Deposit Successful");
    } catch (Exception e) {
        JOptionPane.showMessageDialog(null, e);
    }
}
```

### 4.**Withdrawal**
- **Purpose**:Withdraws a specified amount from the user's account.

    #### Key Methods:
```java
private void WithdrawActionPerformed(java.awt.event.ActionEvent evt) {
    String sql = "update Account set Balance=? where Acc=?";
    try {
        pst = conn.prepareStatement(sql);
        pst.setString(1, NewbalWithdraw.getText());
        pst.setString(2, AccnumWithdraw.getText());
        pst.executeUpdate();
        JOptionPane.showMessageDialog(null, "Withdrawal Successful");
    } catch (Exception e) {
        JOptionPane.showMessageDialog(null, e);
    }
}
```

### 5.**View Balance**
- **Purpose**: Retrieves the balance of a specified account.

    #### Key Methods:
```java
private void SearchVBActionPerformed(java.awt.event.ActionEvent evt) {
    String sql = "select * from Account where Acc=?";
    try {
        pst = conn.prepareStatement(sql);
        pst.setString(1, AccnumVB.getText());
        rs = pst.executeQuery();
        if (rs.next()) {
            FullnameVB.setText(rs.getString("Name"));
            MnumVB.setText(rs.getString("MICR_No"));
            BalVB.setText(rs.getString("Balance"));
        } else {
            JOptionPane.showMessageDialog(null, "Account Not Found");
        }
    } catch (Exception e) {
        JOptionPane.showMessageDialog(null, e);
    }
}
```
### 6.**Change PIN**
- **Purpose**:Changes the account's PIN for security purposes.

    #### Key Methods:
```java
private void ChangepinActionPerformed(java.awt.event.ActionEvent evt) {
    String sql = "update Account set Pin=? where Acc=?";
    try {
        pst = conn.prepareStatement(sql);
        pst.setString(1, NewpinChange.getText());
        pst.setString(2, OldpinChange.getText());
        pst.executeUpdate();
        JOptionPane.showMessageDialog(null, "PIN changed successfully");
    } catch (Exception e) {
        JOptionPane.showMessageDialog(null, e);
    }
}
```

### 7.**Profile Edit**
- **Purpose**:Edits and updates the profile details of the user.

    #### Key Methods:
```java
private void SaveProfileActionPerformed(java.awt.event.ActionEvent evt) {
    String sql = "update Account set Name=?, Address=?, Mob=?, Ethnicity=?, Gender=?, DOB=? where Acc=?";
    try {
        pst = conn.prepareStatement(sql);
        pst.setString(1, FullnameProfile.getText());
        pst.setString(2, AddressProfile.getText());
        pst.setString(3, MobileProfile.getText());
        pst.setString(4, EthnicityProfile.getText());
        pst.setString(5, GenderProfile.getText());
        pst.setString(6, DateofBirthProfile.getText());
        pst.setString(7, AccnumProfile.getText());
        pst.executeUpdate();
        JOptionPane.showMessageDialog(null, "Profile Updated");
    } catch (Exception e) {
        JOptionPane.showMessageDialog(null, e);
    }
}
```
This repo is for the  UQU software documentation course.
