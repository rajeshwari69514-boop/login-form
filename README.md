# login-form

# Coding
<!DOCTYPE html>
<html>
<head>
    <title>Student Management System</title>
    <style>
        body {
            margin: 0;
            font-family: Arial, sans-serif;
            background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }

        .box {
            width: 95%;
            max-width: 950px;
            padding: 30px;
            border-radius: 20px;
            background: rgba(255, 255, 255, 0.08);
            backdrop-filter: blur(15px);
            -webkit-backdrop-filter: blur(15px);
            border: 1px solid rgba(255, 255, 255, 0.2);
            box-shadow: 0 0 30px rgba(0, 255, 255, 0.2);
            color: white;
        }

        h2 {
            text-align: center;
            margin-bottom: 20px;
            background: linear-gradient(90deg, #00f2fe, #4facfe);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        input, select {
            width: 100%;
            padding: 10px;
            margin: 8px 0;
            border-radius: 8px;
            border: 1px solid rgba(255,255,255,0.3);
            background: rgba(255,255,255,0.1);
            color: white;
            font-weight: 500;
        }

        input::placeholder {
            color: #ddd;
        }

        input:focus, select:focus {
            outline: none;
            border: 1px solid #00f2fe;
            box-shadow: 0 0 10px #00f2fe;
        }

        button {
            padding: 9px 15px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 14px;
            margin: 4px 2px;
            color: white;
            background: linear-gradient(90deg, #00f2fe, #4facfe);
            transition: 0.3s;
        }

        button:hover {
            transform: scale(1.05);
            box-shadow: 0 0 15px #00f2fe;
        }

        .logout-btn {
            background: linear-gradient(90deg, #ff416c, #ff4b2b);
            width: 100%;
        }

        table {
            width: 100%;
            margin-top: 15px;
            border-collapse: collapse;
        }

        th, td {
            border: 1px solid rgba(255,255,255,0.2);
            padding: 8px;
            text-align: center;
        }

        th {
            background: linear-gradient(90deg, #00f2fe, #4facfe);
            color: black;
        }

        td {
            color: #ffffff;
        }

        .hidden {
            display: none;
        }
    </style>
</head>
<body>

<div class="box" id="loginBox">
    <h2>🔐 Login</h2>
    <input type="text" id="username" placeholder="Enter Username">
    <input type="password" id="password" placeholder="Enter Password">
    <button onclick="login()">Login</button>
</div>

<div class="box hidden" id="studentBox">
    <h2>🎓 Student Registration</h2>

    <input type="hidden" id="editIndex">

    <input type="text" id="name" placeholder="Full Name">
    <input type="text" id="roll" placeholder="Roll Number">

    <select id="dept">
        <option value="">Select Department</option>
        <option>CSE</option>
        <option>IT</option>
        <option>ECE</option>
        <option>EEE</option>
        <option>Mechanical</option>
        <option>Civil</option>
        <option>AIML</option>
    </select>

    <select id="gender">
        <option value="">Select Gender</option>
        <option>Male</option>
        <option>Female</option>
        <option>Other</option>
    </select>

    <input type="text" id="contact" placeholder="Contact Number">

    <button onclick="saveStudent()">Save Student</button>
    <button class="logout-btn" onclick="logout()">Logout</button>

    <table>
        <thead>
            <tr>
                <th>Name</th>
                <th>Roll</th>
                <th>Dept</th>
                <th>Gender</th>
                <th>Contact</th>
                <th style="width:130px;">Action</th>
            </tr>
        </thead>
        <tbody id="studentTable"></tbody>
    </table>
</div>

<script>
    let students = JSON.parse(localStorage.getItem("students")) || [];

    function login() {
        if (username.value === "admin" && password.value === "1234") {
            loginBox.classList.add("hidden");
            studentBox.classList.remove("hidden");
            displayStudents();
        } else {
            alert("Invalid Username or Password!");
        }
    }

    function logout() {
        loginBox.classList.remove("hidden");
        studentBox.classList.add("hidden");
    }

    function saveStudent() {
        let editIndex = document.getElementById("editIndex").value;

        let student = {
            name: name.value,
            roll: roll.value,
            dept: dept.value,
            gender: gender.value,
            contact: contact.value
        };

        if (editIndex === "") {
            students.push(student);
        } else {
            students[editIndex] = student;
        }

        localStorage.setItem("students", JSON.stringify(students));
        clearForm();
        displayStudents();
    }

    function displayStudents() {
        studentTable.innerHTML = "";
        students.forEach((s, index) => {
            studentTable.innerHTML += `
                <tr>
                    <td>${s.name}</td>
                    <td>${s.roll}</td>
                    <td>${s.dept}</td>
                    <td>${s.gender}</td>
                    <td>${s.contact}</td>
                    <td>
                        <button onclick="editStudent(${index})">Edit</button>
                        <button onclick="deleteStudent(${index})"
                        style="background:linear-gradient(90deg,#ff416c,#ff4b2b);">
                        Delete</button>
                    </td>
                </tr>
            `;
        });
    }

    function editStudent(index) {
        let s = students[index];
        name.value = s.name;
        roll.value = s.roll;
        dept.value = s.dept;
        gender.value = s.gender;
        contact.value = s.contact;
        editIndex.value = index;
    }

    function deleteStudent(index) {
        students.splice(index, 1);
        localStorage.setItem("students", JSON.stringify(students));
        displayStudents();
    }

    function clearForm() {
        name.value = "";
        roll.value = "";
        dept.value = "";
        gender.value = "";
        contact.value = "";
        editIndex.value = "";
    }
</script>

</body>
</html>

# Website

<img width="1262" height="536" alt="image" src="https://github.com/user-attachments/assets/eb575aa7-0206-425e-b65b-38ecc2f9ccb9" />
<img width="1217" height="773" alt="image" src="https://github.com/user-attachments/assets/33fba046-8f16-47f7-96b5-50bb4212c76b" />



# Output
 https://rajeshwari69514-boop.github.io/login-form/
