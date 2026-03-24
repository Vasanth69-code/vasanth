# vasanth1. Develop a Servlet program that accepts student name and register number and displays them in the browser.


2. Develop a Servlet program that uses POST method to store user login details.


3. Write a Servlet program that creates a session and displays the session ID.


4. Write a Servlet program that stores a user name in a cookie and retrieves it.


5. Develop a Servlet program to insert student data into a database using JDBC.


6. Write a program that connects to a database and retrieves student details using JDBC.


7. Develop a simple login page using Servlet and session handling.


8. Write a Servlet program that accepts marks of a student and displays the total and average.


Nice 👍 this is a full Servlet + JDBC lab set. I’ll give you clean, exam-ready programs for each question with simple explanations so you can write in record + viva.
✅ 1. Servlet to Accept Student Name & Register Number
HTML Form
Copy code
Html
<form action="StudentServlet" method="get">
    Name: <input type="text" name="name"><br>
    Reg No: <input type="text" name="regno"><br>
    <input type="submit" value="Submit">
</form>
Servlet
Copy code
Java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class StudentServlet extends HttpServlet {
    public void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
        response.setContentType("text/html");

        String name = request.getParameter("name");
        String regno = request.getParameter("regno");

        PrintWriter out = response.getWriter();
        out.println("<h2>Student Details</h2>");
        out.println("Name: " + name + "<br>");
        out.println("Register Number: " + regno);
    }
}
✅ 2. Servlet using POST for Login
HTML
Copy code
Html
<form action="LoginServlet" method="post">
    Username: <input type="text" name="user"><br>
    Password: <input type="password" name="pass"><br>
    <input type="submit" value="Login">
</form>
Servlet
Copy code
Java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class LoginServlet extends HttpServlet {
    public void doPost(HttpServletRequest req, HttpServletResponse res) throws IOException {
        res.setContentType("text/html");

        String user = req.getParameter("user");
        String pass = req.getParameter("pass");

        PrintWriter out = res.getWriter();
        out.println("Username: " + user + "<br>");
        out.println("Password: " + pass);
    }
}
✅ 3. Session Creation & Display Session ID
Copy code
Java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class SessionServlet extends HttpServlet {
    public void doGet(HttpServletRequest req, HttpServletResponse res) throws IOException {
        res.setContentType("text/html");

        HttpSession session = req.getSession();
        String id = session.getId();

        PrintWriter out = res.getWriter();
        out.println("Session ID: " + id);
    }
}
✅ 4. Cookie Store & Retrieve Username
Copy code
Java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class CookieServlet extends HttpServlet {
    public void doGet(HttpServletRequest req, HttpServletResponse res) throws IOException {
        res.setContentType("text/html");

        String username = "Vasanth";

        // Store cookie
        Cookie c = new Cookie("user", username);
        res.addCookie(c);

        // Retrieve cookie
        Cookie[] cookies = req.getCookies();
        PrintWriter out = res.getWriter();

        for (Cookie cookie : cookies) {
            if (cookie.getName().equals("user")) {
                out.println("Username from Cookie: " + cookie.getValue());
            }
        }
    }
}
✅ 5. Insert Student Data using JDBC
Copy code
Java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import java.sql.*;

public class InsertServlet extends HttpServlet {
    public void doPost(HttpServletRequest req, HttpServletResponse res) throws IOException {
        res.setContentType("text/html");

        String name = req.getParameter("name");
        String regno = req.getParameter("regno");

        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
            Connection con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/studentdb", "root", "password");

            PreparedStatement ps = con.prepareStatement(
                "INSERT INTO student VALUES (?, ?)");

            ps.setString(1, name);
            ps.setString(2, regno);

            ps.executeUpdate();

            PrintWriter out = res.getWriter();
            out.println("Data Inserted Successfully");

            con.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
✅ 6. Retrieve Student Data using JDBC
Copy code
Java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import java.sql.*;

public class RetrieveServlet extends HttpServlet {
    public void doGet(HttpServletRequest req, HttpServletResponse res) throws IOException {
        res.setContentType("text/html");

        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
            Connection con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/studentdb", "root", "password");

            Statement st = con.createStatement();
            ResultSet rs = st.executeQuery("SELECT * FROM student");

            PrintWriter out = res.getWriter();

            while (rs.next()) {
                out.println("Name: " + rs.getString(1) + "<br>");
                out.println("Reg No: " + rs.getString(2) + "<br><br>");
            }

            con.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
✅ 7. Login Page using Session
Copy code
Java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class LoginSessionServlet extends HttpServlet {
    public void doPost(HttpServletRequest req, HttpServletResponse res) throws IOException {
        res.setContentType("text/html");

        String user = req.getParameter("user");

        HttpSession session = req.getSession();
        session.setAttribute("username", user);

        PrintWriter out = res.getWriter();
        out.println("Welcome " + user);
        out.println("<br>Session Created");
    }
}
✅ 8. Calculate Total & Average Marks
Copy code
Java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class MarksServlet extends HttpServlet {
    public void doPost(HttpServletRequest req, HttpServletResponse res) throws IOException {
        res.setContentType("text/html");

        int m1 = Integer.parseInt(req.getParameter("m1"));
        int m2 = Integer.parseInt(req.getParameter("m2"));
        int m3 = Integer.parseInt(req.getParameter("m3"));

        int total = m1 + m2 + m3;
        double avg = total / 3.0;

        PrintWriter out = res.getWriter();
        out.println("Total: " + total + "<br>");
        out.println("Average: " + avg);
    }
}
💡 
