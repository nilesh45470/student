<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Student Information System</title>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&family=Open+Sans:wght@400;600&display=swap" rel="stylesheet">
    <style>
        /* General Body Styles */
        body {
            font-family: 'Open Sans', sans-serif;
            padding: 20px;
            background-color: #e9f2f7; /* Lighter blue background */
            color: #333;
            line-height: 1.6;
            box-shadow: 0 0 25px rgba(0,0,0,0.1); /* Softer shadow */
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: flex-start;
            align-items: center;
            border-radius: 15px; /* Slightly rounded body */
            overflow-x: hidden; /* Ensures shadow is contained, prevent horizontal scroll */
            width: 100%; /* Ensure body takes full width */
            box-sizing: border-box; /* Include padding in width calculation */
        }

        /* Header Styles */
        h2 {
            text-align: center;
            color: #1a73e8; /* Google Blue */
            margin-bottom: 35px;
            font-weight: 700;
            font-family: 'Roboto', sans-serif;
            text-shadow: 1px 1px 3px rgba(0,0,0,0.15); /* More pronounced shadow */
            letter-spacing: 0.5px;
        }

        /* Search Container Styles */
        #searchContainer {
            background-color: #ffffff;
            padding: 30px;
            border-radius: 12px;
            box-shadow: 0 6px 20px rgba(0, 0, 0, 0.12); /* Stronger, softer shadow */
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            gap: 20px; /* Increased gap */
            margin-bottom: 40px;
            flex-wrap: wrap;
            width: 100%;
            max-width: 650px; /* Slightly wider */
            border: 1px solid #e0e0e0; /* Subtle border */
        }

        #studentNameInput {
            width: 100%;
            max-width: 450px; /* Wider input */
            padding: 14px 18px; /* Larger padding */
            border: 2px solid #a8d5ff; /* Lighter blue border */
            border-radius: 9px;
            font-size: 1.05em; /* Slightly larger font */
            transition: all 0.3s ease;
            box-sizing: border-box; /* Include padding in width */
        }

        #studentNameInput:focus {
            border-color: #1a73e8; /* Focus color Google Blue */
            box-shadow: 0 0 0 0.25rem rgba(26, 115, 232, 0.3); /* Google blue glow */
            outline: none;
        }

        #searchContainer button {
            background-color: #1a73e8; /* Google Blue */
            color: white;
            padding: 14px 30px; /* Larger padding */
            border: none;
            border-radius: 9px;
            cursor: pointer;
            font-size: 1.05em; /* Slightly larger font */
            font-weight: 600; /* Medium bold */
            transition: background-color 0.3s ease, transform 0.2s ease;
            width: 100%;
            max-width: 220px;
        }

        #searchContainer button:hover {
            background-color: #0d47a1; /* Darker blue on hover */
            transform: translateY(-3px); /* More pronounced lift */
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }

        #searchContainer button:active {
            transform: translateY(0);
            box-shadow: none;
        }

        /* Search Results Container Styles */
        #searchResults {
            margin-top: 30px;
            padding: 25px 30px;
            border-radius: 12px;
            background-color: #ffffff;
            box-shadow: 0 5px 18px rgba(0, 0, 0, 0.1); /* Softer shadow */
            display: none; /* Initial state hidden */
            opacity: 0;
            transition: opacity 0.4s ease-in-out, transform 0.4s ease-in-out;
            transform: translateY(15px);
            width: 100%;
            max-width: 850px; /* Wider results */
            border: 1px solid #e0e0e0;
        }

        /* When visible */
        #searchResults.visible {
            display: block;
            opacity: 1;
            transform: translateY(0);
        }

        #searchResults h3 {
            color: #1a73e8;
            margin-top: 0;
            margin-bottom: 20px;
            font-size: 1.4em; /* Larger heading */
            text-align: center;
            font-weight: 700;
        }

        #searchResults ul {
            list-style: none;
            padding: 0;
            max-height: 280px; /* Taller scroll area */
            overflow-y: auto; /* Enable vertical scroll */
            border-top: 1px solid #eee; /* Separator */
            padding-top: 10px;
        }

        #searchResults ul li {
            background-color: #f7fcff; /* Very light blue for items */
            margin-bottom: 10px; /* More spacing */
            padding: 12px 20px; /* More padding */
            border-radius: 8px;
            cursor: pointer;
            transition: background-color 0.3s ease, transform 0.2s ease;
            border: 1px solid #d0e7f7; /* Lighter border */
            font-size: 1.0em;
        }

        #searchResults ul li:hover {
            background-color: #e6f3fa; /* Slightly darker hover */
            transform: translateX(5px); /* Slide effect */
        }

        /* Student Profile Display Styles */
        #studentProfile {
            margin-top: 30px;
            border: 1px solid #1a73e8; /* Google blue border */
            padding: 30px 35px; /* More padding */
            border-radius: 12px;
            background-color: #eaf6ff; /* Lighter background for profile */
            box-shadow: 0 6px 20px rgba(0, 0, 0, 0.12);
            min-height: 120px;
            display: none; /* Initial state hidden */
            flex-direction: column;
            justify-content: center;
            align-items: flex-start;
            position: relative;
            width: 100%;
            max-width: 850px; /* Wider profile */
        }
        
        #studentProfile.visible {
            display: flex; /* Make it visible and use flex layout */
        }

        #studentProfile h3 {
            color: #0d47a1; /* Darker blue for profile heading */
            margin-top: 0;
            margin-bottom: 20px;
            font-size: 1.6em; /* Larger heading */
            width: 100%;
            text-align: center;
            font-family: 'Roboto', sans-serif;
        }

        .profile-field {
            display: flex;
            align-items: center;
            margin-bottom: 12px; /* More spacing */
            width: 100%;
            flex-wrap: wrap;
            font-size: 1.05em; /* Slightly larger text */
        }

        .profile-field strong {
            color: #1a73e8; /* Google blue for labels */
            min-width: 160px; /* Wider labels */
            display: inline-block;
            font-weight: 600; /* Medium bold */
        }

        .profile-field span {
            flex-grow: 1;
            padding: 8px 10px; /* Padding for display text */
            border: 1px solid #cceeff; /* Light blue border */
            border-radius: 6px;
            background-color: #f0f8ff; /* Very light blue background */
        }
        
        .profile-actions {
            margin-top: 25px; /* More margin */
            text-align: center;
            width: 100%;
            border-top: 1px solid #e0e0e0; /* Separator line */
            padding-top: 20px;
        }

        .profile-actions button.close-btn {
            background-color: #607d8b; /* Greyish blue for close button */
            color: white;
            padding: 12px 25px;
            border: none;
            border-radius: 9px;
            cursor: pointer;
            font-size: 1.0em;
            font-weight: 600;
            transition: background-color 0.3s ease, transform 0.2s ease;
            margin: 0 5px;
        }

        .profile-actions button.close-btn:hover {
            background-color: #455a64; /* Darker greyish blue on hover */
            transform: translateY(-2px);
        }

        .profile-actions button.close-btn:active {
            transform: translateY(0);
            box-shadow: none;
        }
        
        /* Table Styles */
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 40px;
            box-shadow: 0 6px 20px rgba(0, 0, 0, 0.12); /* Stronger shadow */
            border-radius: 12px;
            overflow: hidden; /* Ensures rounded corners */
            background-color: #ffffff;
        }

        th, td {
            border: 1px solid #e0e0e0;
            padding: 14px 18px; /* More padding */
            text-align: left;
            font-size: 0.95em;
        }

        th {
            background-color: #1a73e8; /* Google Blue */
            color: white;
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 0.08em; /* Slightly wider spacing */
            position: sticky;
            top: 0;
            z-index: 1;
            font-family: 'Roboto', sans-serif;
        }

        tr:nth-child(even) {
            background-color: #f7fafd; /* Very light blue for even rows */
        }

        tr:hover {
            background-color: #e6f3fa; /* Light blue on hover */
            cursor: pointer;
            box-shadow: inset 3px 0 0 #1a73e8; /* Left border highlight on hover */
        }

        /* Scrollbar styles for tables and search results */
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }

        ::-webkit-scrollbar-track {
            background: #f1f1f1;
            border-radius: 10px;
        }

        ::-webkit-scrollbar-thumb {
            background: #888;
            border-radius: 10px;
        }

        ::-webkit-scrollbar-thumb:hover {
            background: #555;
        }

        .table-container {
            width: 100%;
            margin-top: 40px;
        }

        /* Responsive Design for smaller screens */
        @media (max-width: 768px) {
            body {
                padding: 10px;
                max-width: 100%;
                box-shadow: none;
                border-radius: 0;
            }
            h2 {
                font-size: 1.8em;
                margin-bottom: 25px;
            }
            #searchContainer, #searchResults, #studentProfile {
                padding: 15px;
                max-width: 100%;
                border-radius: 8px;
                box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
            }
            #searchContainer {
                flex-direction: column;
                gap: 10px;
            }
            #studentNameInput, #searchContainer button {
                max-width: 100%;
                padding: 10px 12px;
                font-size: 0.95em;
            }
            th, td {
                padding: 10px;
                font-size: 0.85em;
            }
            th:nth-child(2), td:nth-child(2) { min-width: 180px; }
            th:nth-child(3), td:nth-child(3) { min-width: 150px; }
            th:nth-child(8), td:nth-child(8) { min-width: 180px; }
            th:nth-child(9), td:nth-child(9) { min-width: 120px; }
            th:nth-child(10), td:nth-child(10) { min-width: 120px; } /* Date of Birth column */

            .profile-field {
                flex-direction: column;
                align-items: flex-start;
                margin-bottom: 8px;
            }
            .profile-field strong {
                min-width: unset;
                margin-bottom: 5px;
            }
            .profile-field span {
                width: 100%;
                margin-left: 0;
                box-sizing: border-box;
            }
            .profile-actions button.close-btn {
                margin-top: 10px;
                width: auto;
                padding: 10px 20px;
            }
        }
    </style>
</head>
<body>

    <h2>Student Information System</h2>

    <div id="searchContainer">
        <input type="text" id="studentNameInput" placeholder="Enter Name, PRN, Email or Mobile No." onkeyup="handleSearchInput(event)">
        <button onclick="searchStudent()">Search Student</button>
    </div>

    <div id="searchResults"></div>

    <div id="studentProfile">
        <h3>Select a Student</h3>
        <p>Click on a student from the search results or the list below to view their details.</p>
    </div>

    <div class="table-container">
        <table>
            <thead>
                <tr>
                    <th>SR.No.</th>
                    <th>Name</th>
                    <th>Address</th>
                    <th>Category</th>
                    <th>Class</th>
                    <th>PRN No.</th>
                    <th>Blood Group</th>
                    <th>Email ID</th>
                    <th>MO.NO.</th>
                    <th>Date of Birth</th>
                </tr>
            </thead>
            <tbody id="studentTableBody">
                <tr><td>1</td><td>Aaware Prajakta Anil</td><td>Shindi</td><td>OBC</td><td>FYBsc</td><td>2024015400331491</td><td>O+</td><td>prajaktaaware684@gmail.com</td><td>8600951543</td><td>07 June 2006</td></tr>
                <tr><td>2</td><td>Agnihotri Sanyukta Laxmikant</td><td></td><td></td><td>FYBsc</td><td>2024015400336526</td><td></td><td></td><td></td><td>22 April 2005</td></tr>
                <tr><td>3</td><td>Ahire Gaurav Ganesh</td><td>Waghdu</td><td>OBC</td><td>FYBsc</td><td>2024015400350252</td><td>B+</td><td>ahire623@gmail.com</td><td>9529759898</td><td></td></tr>
                <tr><td>4</td><td>Ahire Harshadada Nana</td><td>Mehunbare</td><td>SC</td><td>FYBsc</td><td>2024015400331219</td><td>O+</td><td>harshadaa213@gmail.com</td><td>7822866539</td><td></td></tr>
                <tr><td>5</td><td>Ahire Kunal Bapu</td><td>Ranjangaon</td><td>SC</td><td>FYBsc</td><td>2024015400332076</td><td>B+</td><td>kunalahire283@gmail.com</td><td>9561244610</td><td>17 March 2007</td></tr>
                <tr><td>6</td><td>Ahire Rutuja Satish</td><td>Tambhole</td><td>OBC</td><td>FYBsc</td><td>2024015400353045</td><td>B+</td><td>rg322700701@gmail.com</td><td>9322700701</td><td></td></tr>
                <tr><td>7</td><td>Ahirrao Amruta Himmat</td><td>Khadakiseem</td><td>OBC</td><td>FYBsc</td><td>2024015400331556</td><td>O+</td><td>krishnaahirao832@gmail.com</td><td>7447504352</td><td></td></tr>
                <tr><td>8</td><td>Andholkar Srushti Vinod</td><td>Chalisgaon</td><td>OBC</td><td>FYBsc</td><td>2024015400342287</td><td>B+</td><td>srushtiandholkar@gmail.com</td><td>8975826609</td><td></td></tr>
                <tr><td>9</td><td>Atif Khan Nasir Khan</td><td>Chalisgaon</td><td>UR</td><td>FYBsc</td><td>2024015400350492</td><td></td><td>khanaatef37@gmail.com</td><td>7507860933</td><td></td></tr>
                <tr><td>10</td><td>Baig Saniya Mirza Amjad Baig</td><td></td><td></td><td>FYBsc</td><td>2024015400342322</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>11</td><td>Baig Zafar Abdul Wahed</td><td></td><td></td><td>FYBsc</td><td>2024015400351762</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>12</td><td>Bairagi Sakshi Dharmadas</td><td></td><td></td><td>FYBsc</td><td>2024015400342562</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>13</td><td>Bangale Vaidhahi Vijay</td><td>Waghali</td><td>OBC</td><td>FYBsc</td><td>2024015400342411</td><td>O+</td><td>vaidhahibangale3@gmail.com</td><td>7030682101</td><td></td></tr>
                <tr><td>14</td><td>Barve Pallavi Bausaheb</td><td>Shindi</td><td>OBC</td><td>FYBsc</td><td>2024015400331413</td><td>O+</td><td>bhausahebbarve888@gmail.com</td><td>9503842980</td><td>03 July 2007</td></tr>
                <tr><td>15</td><td>Bhalerao Diksha Ganesh</td><td></td><td></td><td>FYBsc</td><td>2024015400350372</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>16</td><td>Bhoite Tulsi Mahendra</td><td>Bhavali</td><td></td><td>FYBsc</td><td>2024015400331107</td><td>B+</td><td></td><td>9370412557</td><td></td></tr>
                <tr><td>17</td><td>Birari Rushikesh Ravindra</td><td>Nagardeola</td><td>OBC</td><td>FYBsc</td><td>2024015400342426</td><td>A+</td><td>patilrushikeshr5@gmail.com</td><td>9209275700</td><td></td></tr>
                <tr><td>18</td><td>Borse Gayatri Gorakshanath</td><td>Daskebardi</td><td>OBC</td><td>FYBsc</td><td>2024015400342264</td><td>B+</td><td>gorakhborse149@gmail.com</td><td>9511825138</td><td></td></tr>
                <tr><td>19</td><td>Chaudhari Tejashree Chandrakant</td><td></td><td></td><td>FYBsc</td><td>2024015400330038</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>20</td><td>Chavan Chetan Nandkishor</td><td></td><td></td><td>FYBsc</td><td>2024015400331483</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>21</td><td>Chavan Gayatri Aaba</td><td>Pimparkheda</td><td>OBC</td><td>FYBsc</td><td>2024015400347741</td><td>O+</td><td>atul14486@gmail.com</td><td>7776015275</td><td></td></tr>
                <tr><td>22</td><td>Chavan Prem Anil</td><td></td><td></td><td>FYBsc</td><td>2024015400330166</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>23</td><td>Chavan Sakshi Kiran</td><td>Hingone</td><td>OBC</td><td>FYBsc</td><td>2024015400352452</td><td>A+</td><td>kiranchvan019990@gmail.com</td><td></td><td>03 October 2005</td></tr>
                <tr><td>24</td><td>Chavan Sandesh Vinayakrao</td><td>Ranjangaon</td><td></td><td>FYBsc</td><td>2024015400330069</td><td></td><td></td><td></td><td></td></tr> 
                <tr><td>25</td><td>Chavhan Rohit Ratilal</td><td>Bhadgaon</td><td>OBC</td><td>FYBsc</td><td>2024015400331692</td><td>O-</td><td>chavenratilal@gmail.com</td><td>8806768055</td><td></td></tr>
                <tr><td>26</td><td>Daund Pratiksha Ganesh</td><td>Shindi</td><td></td><td>FYBsc</td><td>2024015400347691</td><td>B+</td><td>pratikshadaund09@gmail.com</td><td>8407970578</td><td></td></tr>
                <tr><td>27</td><td>Deokar Asmita Narayan</td><td>Palasare</td><td></td><td>FYBsc</td><td>2024015400330093</td><td></td><td>asmitadeokar5@gmail.com</td><td>8407970578</td><td></td></tr>
                <tr><td>28</td><td>Deokar Hitesh Dattatray</td><td>Nandgaon</td><td>OBC</td><td>FYBsc</td><td>2024015400350414</td><td>AB+</td><td>hiteshdeokar143@gmail.com</td><td>8668325979</td><td></td></tr>
                <tr><td>29</td><td>Deokar Shubhangi Sunilrao</td><td>Palasare</td><td>SBC</td><td>FYBsc</td><td>2024015400330576</td><td>A+</td><td>shybangideokar80@gmail.com</td><td>8007271688</td><td></td></tr>
                <tr><td>30</td><td>Deore Devyani Bhimsing</td><td>Pimpri</td><td></td><td>FYBsc</td><td>2024015400331274</td><td>A+</td><td>bhimsingdeokar@gmail.com</td><td>8766981767</td><td></td></tr>
                <tr><td>31</td><td>Deore Sakshi Pradip</td><td>Kargaon</td><td></td><td>FYBsc</td><td>2024015400331081</td><td>A+</td><td>pradipdeore0007@gmail.com</td><td>9850279436</td><td></td></tr>
                <tr><td>32</td><td>Desale Tanmay Diliprao</td><td>Bramanshevga</td><td>OBC</td><td>FYBsc</td><td>2024015400350484</td><td></td><td>desaleking5132@gmail.com</td><td>9307210232</td><td></td></tr>
                <tr><td>33</td><td>Deshmukh Jayashree Umeshrao</td><td></td><td></td><td>FYBsc</td><td>2024015400331121</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>34</td><td>Deshmukh Kalyani Hemant</td><td>Mehunbare</td><td></td><td>FYBsc</td><td>2024015400330085</td><td>O+</td><td>hemantdeshmukh5498@gmail.com</td><td>8446778580</td><td></td></tr>
                <tr><td>35</td><td>Deshmukh Sai Sanjay</td><td></td><td></td><td>FYBsc</td><td>2024015400331452</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>36</td><td>Dhangar Aniket Dipak</td><td></td><td></td><td>FYBsc</td><td>2024015400342515</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>37</td><td>Dhangar Chetana Somnath</td><td></td><td></td><td>FYBsc</td><td>2024015400352444</td><td></td><td></td><td></td><td>29 December 2006</td></tr>
                <tr><td>38</td><td>Dhangar Shishupal Nimba</td><td>Akhatwade</td><td>DTNT</td><td>FYBsc</td><td>2024015400336573</td><td>O+</td><td>dhangarvijaya1@gmail.com</td><td>7498239474</td><td></td></tr>
                <tr><td>39</td><td>Dusane Diksha Sunil</td><td></td><td></td><td>FYBsc</td><td>2024015400331564</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>40</td><td>Gaikwad Disha Bhanudas</td><td></td><td></td><td>FYBsc</td><td>2024015400330611</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>41</td><td>Gaikwad Komal Prakash</td><td>Pimparkheda</td><td>OBC</td><td>FYBsc</td><td>2024015400331637</td><td>O+</td><td>komalgaikwaqd02@gmail.com</td><td>8805529988</td><td></td></tr>
                <tr><td>42</td><td>Gawali Chaitanya Anil</td><td></td><td></td><td>FYBsc</td><td>2024015400330626</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>43</td><td>Gawali Prachi Kishor</td><td></td><td></td><td>FYBsc</td><td>2024015400331018</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>44</td><td>Gawali Pravin Dattu</td><td></td><td></td><td>FYBsc</td><td>2024015400350317</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>45</td><td>Gore Siddhi Pradip</td><td>Chalisgaon</td><td>OBC</td><td>FYBsc</td><td>2024015400331517</td><td>A+</td><td>siddhipagare678@gmail.com</td><td>7387762134</td><td></td></tr>
                <tr><td>46</td><td>Gore Vedant Amol</td><td></td><td></td><td>FYBsc</td><td>2024015400341632</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>47</td><td>Gosavi Mansi Ramchandra</td><td>Chalisgaon</td><td>OBC</td><td>FYBsc</td><td>2024015400331177</td><td>B+</td><td>mansigosavi3172006@gmail.com</td><td>9850329811</td><td></td></tr>
                <tr><td>48</td><td>Ingale Ganesh Satish</td><td>Hirapur</td><td></td><td>FYBsc</td><td>2024015400342306</td><td>B+</td><td>ganeshingale9309@gmail.com</td><td>9356802851</td><td></td></tr>
                <tr><td>49</td><td>Jadhav Chitali Aaba</td><td>Mundkheda</td><td></td><td>FYBsc</td><td>2024015400347613</td><td>O+</td><td></td><td>9970972201</td><td></td></tr>
                <tr><td>50</td><td>Jadhav Chitali Ekhanath</td><td>Tambhole</td><td>OBC</td><td>FYBsc</td><td>2024015400342272</td><td>B+</td><td>jadhavkuldip62@gmail.com</td><td>8767373411</td><td></td></tr>
                <tr><td>51</td><td>Jadhav Premkumar Pandurang</td><td>Pimparkheda</td><td>OBC</td><td>FYBsc</td><td>2024015400331049</td><td></td><td>premjadhav9373@gmail.com</td><td>9373295729</td><td></td></tr>
                <tr><td>52</td><td>Jadhav Poonam Madan</td><td>Bilakhed</td><td>SC</td><td>FYBsc</td><td>2024015400347497</td><td>A+</td><td></td><td>9209466642</td><td></td></tr>
                <tr><td>53</td><td>Jadhav Sakshi Ravindra</td><td></td><td></td><td>FYBsc</td><td>2024015400331997</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>54</td><td>Jadhav Yash Vijay</td><td>Chalisgaon</td><td>SC</td><td>FYBsc</td><td>2024015400332001</td><td>B+</td><td>premjadhav9373@gmail.com</td><td>8237204091</td><td></td></tr>
                <tr><td>55</td><td>Jagtap Chaitali Dagadu</td><td>Pimparkheda</td><td>OBC</td><td>FYBsc</td><td>2024015400342376</td><td>O+</td><td>chaitalijagtap2103@gmail.com</td><td>7620662706</td><td></td></tr>
                <tr><td>56</td><td>Jagtap Roshani Anil</td><td></td><td></td><td>FYBsc</td><td>2024015400351754</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>57</td><td>Kadam Samir Sadu</td><td></td><td></td><td>FYBsc</td><td>2024015400342105</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>58</td><td>Kapdane Vaishnavi Aniln</td><td>Chalisgaon</td><td>OBC</td><td>FYBsc</td><td>2024015400331297</td><td>B+</td><td>kapadanevaishnavi@gmail.com</td><td>9423344160</td><td>25 April 2006</td></tr>
                <tr><td>59</td><td>Katkar Jayshri Pravin</td><td>Nagardevla</td><td></td><td>FYBsc</td><td>2024015400330051</td><td>AB+</td><td>jayashrikatkar59@gmail.com</td><td>7558658310</td><td></td></tr>
                <tr><td>60</td><td>Kavde Asavari Dipak</td><td>Chitegaon</td><td>OBC</td><td>FYBsc</td><td>2024015400331703</td><td>O+</td><td>dipakkavade4607@gmail.com</td><td>9561283628</td><td></td></tr>
                <tr><td>61</td><td>Khairnar Harshad Bhagwat</td><td></td><td></td><td>FYBsc</td><td>2024015400331227</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>62</td><td>Khan Irfan Khaleel</td><td>Piparkhed</td><td>UR</td><td>FYBsc</td><td>2024015400331332</td><td></td><td>khanirfangt@gmail.com</td><td>8080402813</td><td></td></tr>
                <tr><td>63</td><td>Khan Misbah Firoz</td><td></td><td></td><td>FYBsc</td><td>2024015400347675</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>64</td><td>Khan Samir Akil</td><td></td><td></td><td>FYBsc</td><td>2024015400331974</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>65</td><td>Khan Zulfin Rais</td><td></td><td></td><td>FYBsc</td><td>2024015400331316</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>66</td><td>Khatik Sahil Yunus</td><td>Chalisgaon</td><td>UR</td><td>FYBsc</td><td>2024015400331324</td><td></td><td>khatiksahil9021@gmail.com</td><td>9021891628</td><td>6 June 2005</td></tr>
                <tr><td>67</td><td>Koli Amol Raju</td><td></td><td></td><td>FYBsc</td><td>2024015400330603</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>68</td><td>Koli Samadhan Anil</td><td></td><td></td><td>FYBsc</td><td>2024015400347725</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>69</td><td>Kumavat Jyoti Suresh</td><td>Chalisgaon</td><td>OBC</td><td>FYBsc</td><td>2024015400347377</td><td>AB+</td><td>vidhyakumavat22@gmail.com</td><td>8830183623</td><td></td></tr>
                <tr><td>70</td><td>Kumavat Nandini Somnath</td><td>Beldarvadi</td><td>OBC</td><td>FYBsc</td><td>2024015400332029</td><td>B+</td><td>nanadinikumavat691@gmail.com</td><td>7620579189</td><td></td></tr>
                <tr><td>71</td><td>Kumavat Roshan Sambhaji</td><td></td><td></td><td>FYBsc</td><td>2024015400330762</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>72</td><td>Kumavat Shruti Dipak</td><td></td><td></td><td>FYBsc</td><td>2024015400331266</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>73</td><td>Kumavat Vishakhha Bhausaheb</td><td>Beldarvadi</td><td>DTNT</td><td>FYBsc</td><td>2024015400341624</td><td>B+</td><td>vishakhakumavat580@gmail.com</td><td>9699813541</td><td></td></tr>
                <tr><td>74</td><td>Kuvar Gayatri Bhaiyasaheb</td><td>Khadakiseem</td><td>OBC</td><td>FYBsc</td><td>2024015400347683</td><td>B+</td><td>patilbhaiyyasaheb7@gmail.com</td><td>9970389982</td><td></td></tr>
                <tr><td>75</td><td>Magar Rushikesh Sanjay</td><td></td><td></td><td>FYBsc</td><td>2024015400330077</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>76</td><td>Mahajan Hitesh Sharad</td><td>Bhadgaon</td><td>OBC</td><td>FYBsc</td><td>2024015400331742</td><td>AB+</td><td>sharadmali864@gmail.com</td><td>7767828516</td><td></td></tr>
                <tr><td>77</td><td>Mahajan Kalpesh Santosh</td><td>Nagardevla</td><td></td><td>FYBsc</td><td>2024015400331533</td><td>B+</td><td>kdwarkadhish369@gmail.com</td><td>8550948172</td><td></td></tr>
                <tr><td>78</td><td>Mahajan Nikita Ravindra</td><td>Patonda</td><td>OBC</td><td>FYBsc</td><td>2024015400331676</td><td>B+</td><td>mahajanikita2006@gmail.com</td><td>9503735744</td><td>21 November 2006</td></tr>
                <tr><td>79</td><td>Mahajan Priti Janardhan</td><td>Bhagaon</td><td>OBC</td><td>FYBsc</td><td>2024015400332084</td><td>B+</td><td>deeptijm04@gmail.com</td><td>8459747834</td><td></td></tr>
                <tr><td>80</td><td>Mahajan Roshani Shalik</td><td>Patonda</td><td>OBC</td><td>FYBsc</td><td>2024015400342217</td><td>B+</td><td>mahajanroshani592@gmail.com</td><td>9922707185</td><td>26 December 2005</td></tr>
                <tr><td>81</td><td>Mahajan Saurav Kishor</td><td></td><td></td><td>FYBsc</td><td>2024015400342554</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>82</td><td>Mahale Kirti Indrasing</td><td>Pimpri</td><td></td><td>FYBsc</td><td>2024015400350395</td><td>B-</td><td>kirtimahale09@gmail.com</td><td>9860974116</td><td></td></tr>
                <tr><td>83</td><td>Mali Ghansham Narayan</td><td></td><td></td><td>FYBsc</td><td>2024015400342337</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>84</td><td>Mali Rushikesh Vikas</td><td>Daskebardi</td><td>OBC</td><td>FYBsc</td><td>2024015400350387</td><td></td><td>rushikeshmali274@gmail.com</td><td>8830664245</td><td></td></tr>
                <tr><td>85</td><td>Mali Vaibhavi Kailas</td><td></td><td></td><td>FYBsc</td><td>2024015400342183</td><td></td><td></td><td></td><td>27 January 2006</td></tr>
                <tr><td>86</td><td>Mande Mayuri Dnyaneshwar</td><td>Shindi</td><td>OBC</td><td>FYBsc</td><td>2024015400331467</td><td></td><td>mandem9730@gmail.com</td><td>9730263096</td><td>14 July 2006</td></tr>
                <tr><td>87</td><td>Mande Raj Pandurang</td><td>Shindi</td><td>OBC</td><td>FYBsc</td><td>2024015400342577</td><td>O-</td><td>mandepandurang3@gmail.com</td><td>8788251864</td><td></td></tr>
                <tr><td>88</td><td>Marathe Shaileja Somnath</td><td></td><td></td><td>FYBsc</td><td>2024015400342136</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>89</td><td>Mohammad Danish Shaikh</td><td></td><td></td><td>FYBsc</td><td>2024015400331951</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>90</td><td>Mohim Vishal Rajendra</td><td></td><td></td><td>FYBsc</td><td>2024015400331308</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>91</td><td>Mulla Huneja Ifrajoddin</td><td>Patonda</td><td>OBC</td><td>FYBsc</td><td>2024015400342225</td><td></td><td>mulla.csn.@gmail.com</td><td>7620860031</td><td></td></tr>
                <tr><td>92</td><td>Nerkar Nikhil Madhukar</td><td>Ranjangaon</td><td>OBC</td><td>FYBsc</td><td>2024015400341597</td><td>A+</td><td>nikhilnerkar442@gmail.com</td><td>9021820317</td><td>19 December 2006</td></tr>
                <tr><td>93</td><td>Nevare Vijaya Sharad</td><td></td><td></td><td>FYBsc</td><td>2024015400342314</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>94</td><td>Nikam Kunal Mahendra</td><td>Chinchgavhan</td><td>OBC</td><td>FYBsc</td><td>2024015400330642</td><td>A+</td><td>kunalmahendranikam006@gmail.com</td><td>7620086836</td><td></td></tr>
                <tr><td>95</td><td>Nikam Sakshi Dharmaraj</td><td>Patna</td><td>SC</td><td>FYBsc</td><td>2024015400342295</td><td></td><td>sachindharmaraj9588@gmail.com</td><td></td><td></td></tr>
                <tr><td>96</td><td>Nikumbh Pooja Ravindra</td><td></td><td></td><td>FYBsc</td><td>2024015400331154</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>97</td><td>Padolkar Tejaswini Babulal</td><td>Waghali</td><td>OBC</td><td>FYBsc</td><td>2024015400331111</td><td></td><td>amolsonawane2406@gmail.com</td><td>7385629545</td><td></td></tr>
                <tr><td>98</td><td>Paedeshi Achal Subhash</td><td>Jamda</td><td>OBC</td><td>FYBsc</td><td>2024015400348984</td><td></td><td>kp8789520@gmail.com</td><td>9226598986</td><td></td></tr>
                <tr><td>99</td><td>Pardeshi Alok Chandrakant</td><td>Ranjangaon</td><td>OBC</td><td>FYBsc</td><td>2024015400342403</td><td></td><td></td><td></td><td>16 May 2007</td></tr>
                <tr><td>100</td><td>Pardeshi Kajal Santosh</td><td>Chalisgaon</td><td>DTNT</td><td>FYBsc</td><td>2024015400330584</td><td></td><td></td><td>9960176028</td><td></td></tr>
                <tr><td>101</td><td>Patil Ashwini Rajendra</td><td>Wakadi</td><td>OBC</td><td>FYBsc</td><td>2024015400341616</td><td>AB-</td><td>aash1234patil@gmail.com</td><td>9021973371</td><td></td></tr>
                <tr><td>102</td><td>Patil Bhagyashri Sukhalal</td><td></td><td></td><td>FYBsc</td><td>2024015400352405</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>103</td><td>Patil Dimple Ravindra</td><td>Deoli</td><td>OBC</td><td>FYBsc</td><td>2024015400330101</td><td>AB+</td><td>dimpalpatil1010@gmail.com</td><td>9529949622</td><td></td></tr>
                <tr><td>104</td><td>Patil Divya Bhagwat</td><td></td><td></td><td>FYBsc</td><td>2024015400336542</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>105</td><td>Patil Divya Manohar</td><td>Ozar</td><td>OBC</td><td>FYBsc</td><td>2024015400342604</td><td>A+</td><td>manishamanoharpatil@gmail.com</td><td>9764657280</td><td></td></tr>
                <tr><td>106</td><td>Patil Gayatri Dipak</td><td>Patonda</td><td></td><td>FYBsc</td><td>2024015400350244</td><td>A+</td><td>9p6926395@gmail.com</td><td>9730518034</td><td></td></tr>
                <tr><td>107</td><td>Patil Ghanshyam Bharat</td><td></td><td></td><td>FYBsc</td><td>2024015400331371</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>108</td><td>Patil Gorakhnath Kailas</td><td>Nagradeola</td><td></td><td>FYBsc</td><td>2024015400331595</td><td>B+</td><td>gorakhnathp19@gmail.com</td><td>7058121482</td><td></td></tr>
                <tr><td>109</td><td>Patil Harshada Pravin</td><td></td><td></td><td>FYBsc</td><td>2024015400347501</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>110</td><td>Patil Jagruti Nandan</td><td>Chalisgaon</td><td></td><td>FYBsc</td><td>2024015400330141</td><td></td><td>nandanpatil1982@gmail.com</td><td>9021770253</td><td></td></tr>
                <tr><td>111</td><td>Patil Jayesh Sunil</td><td>Nagardevla</td><td>OBC</td><td>FYBsc</td><td>2024015400342241</td><td>B+</td><td>jp7270779@gmail.com</td><td>7798994464</td><td></td></tr>
                <tr><td>112</td><td>Patil Kalyani Ravindra</td><td>Borkheda</td><td>OBC</td><td>FYBsc</td><td>2024015400331386</td><td>A+</td><td>surekhaahirrao392@gmail.com</td><td>7972706779</td><td></td></tr>
                <tr><td>113</td><td>Patil Kusum Sham</td><td>Londhe</td><td>OBC</td><td>FYBsc</td><td>2024015400342256</td><td>B+</td><td>nileshnikam310@gmail.com</td><td>9834248785</td><td></td></tr>
                <tr><td>114</td><td>Patil Lokesh Vikas</td><td></td><td></td><td>FYBsc</td><td>2024015400331444</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>115</td><td>Patil Mansi Samadhan</td><td></td><td></td><td>FYBsc</td><td>2024015400331347</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>116</td><td>Patil Mansi Sandip</td><td>Malshevaga</td><td>OBC</td><td>FYBsc</td><td>2024015400347636</td><td>O+</td><td>mansipatil92700@gmail.com</td><td></td><td></td></tr>
                <tr><td>117</td><td>Patil Mayuri Arun</td><td>Khadkiseem</td><td>OBC</td><td>FYBsc</td><td>2024015400350437</td><td>A+</td><td>mayurispatil1112@gmail.com</td><td>9860588731</td><td></td></tr>
                <tr><td>118</td><td>Patil Nikita Gonesh</td><td>Chalisgaon</td><td>OBC</td><td>FYBsc</td><td>2024015400331201</td><td>O+</td><td>nikitapatil0305@gmail.com</td><td></td><td></td></tr>
                <tr><td>119</td><td>Patil Nikita Shivaji</td><td></td><td></td><td>FYBsc</td><td>2024015400350476</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>120</td><td>Patil Parth Vijay</td><td>Shindwadi</td><td>VJNT</td><td>FYBsc</td><td>2024015400331235</td><td></td><td></td><td>9322470545</td><td>27 July 2006</td></tr>
                <tr><td>121</td><td>Patil Pavan Pravin</td><td></td><td></td><td>FYBsc</td><td>2024015400342191</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>122</td><td>Patil Payal Manoj</td><td>Kherde</td><td>OBC</td><td>FYBsc</td><td>2024015400331421</td><td>O+</td><td>mp7006472@gmail.com</td><td>9359714705</td><td>4 July 2006</td></tr>
                <tr><td>123</td><td>Patil Pooja Kishor</td><td>Borkheda</td><td>OBC</td><td>FYBsc</td><td>2024015400331502</td><td>A+</td><td>patilpooja47480@gmail.com</td><td>8485881163</td><td></td></tr>
                <tr><td>124</td><td>Patil Pratiksha Bharat</td><td>Borkheda</td><td>OBC</td><td>FYBsc</td><td>2024015400330657</td><td></td><td>patilpratiksha5893@gmail.com</td><td>9503199281</td><td>9 March 2006</td></tr>
                <tr><td>125</td><td>Patil Rahul Ananda</td><td></td><td></td><td>FYBsc</td><td>2024015400331935</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>126</td><td>Patil Raj Prashant</td><td>Deshmukhwadi</td><td>OBC</td><td>FYBsc</td><td>2024015400331436</td><td>A+</td><td>raj880844@gmail.com</td><td>8767902594</td><td></td></tr>
                <tr><td>127</td><td>Patil Sakshi Arun</td><td></td><td></td><td>FYBsc</td><td>2024015400342167</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>128</td><td>Patil Saurav Santosh</td><td>Bhadgaon</td><td>OBC</td><td>FYBsc</td><td>2024015400350445</td><td></td><td>sauravspatil1007@gmail.com</td><td>9158563942</td><td></td></tr>
                <tr><td>129</td><td>Patil Shailesh Pradip</td><td></td><td></td><td>FYBsc</td><td>2024015400330561</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>130</td><td>Patil Shivani Yashavant</td><td></td><td></td><td>FYBsc</td><td>2024015400331572</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>131</td><td>Patil Sneha Sunil</td><td>Chalisgaon</td><td>OBC</td><td>FYBsc</td><td>2024015400331711</td><td>O+</td><td>snehaspatil2022@gmail.com</td><td>9822260216</td><td></td></tr>
                <tr><td>132</td><td>Patil Swami Ambadas</td><td></td><td></td><td>FYBsc</td><td>2024015400331282</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>133</td><td>Patil Swati Nilkanth</td><td></td><td></td><td>FYBsc</td><td>2024015400347702</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>134</td><td>Patil Tanmay Rajesh</td><td></td><td></td><td>FYBsc</td><td>2024015400330021</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>135</td><td>Patil Tanvi Babanrow</td><td>Borkeda</td><td>OBC</td><td>FYBsc</td><td>2024015400341647</td><td>A+</td><td>patiltanvi864@gmail.com</td><td>8010752931</td><td></td></tr>
                <tr><td>136</td><td>Patil Trushna Yogesh</td><td>Bilakhed</td><td>OBC</td><td>FYBsc</td><td>2024015400330119</td><td></td><td>patiltrusha43@gmail.com</td><td>9022769533</td><td></td></tr>
                <tr><td>137</td><td>Patil Vaishnavi Manoher</td><td>Borkeda</td><td>OBC</td><td>FYBsc</td><td>2024015400330158</td><td>B+</td><td>manahorpatil2121@gmail.com</td><td>7387232464</td><td></td></tr>
                <tr><td>138</td><td>Patil Vishal Subhash</td><td></td><td></td><td>FYBsc</td><td>2024015400331525</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>139</td><td>Patil Vivek Samadhan</td><td></td><td></td><td>FYBsc</td><td>2024015400347861</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>140</td><td>Pawar Datta Nagraj</td><td></td><td></td><td>FYBsc</td><td>2024015400331912</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>141</td><td>Pawar Kaveri Hiraman</td><td>Vadgaon</td><td>VJNT</td><td>FYBsc</td><td>2024015400331031</td><td>O+</td><td>hiramanpawar06@gmail.com</td><td></td><td></td></tr>
                <tr><td>142</td><td>Pawar Mahesh Dnyaneshwar</td><td></td><td></td><td>FYBsc</td><td>2024015400347667</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>143</td><td>Pawar Mohini Gorakh</td><td>Nhave</td><td>OBC</td><td>FYBsc</td><td>2024015400347764</td><td>AB+</td><td>gp160138@gmail.com</td><td>9764579308</td><td></td></tr>
                <tr><td>144</td><td>Pawar Puja Dattatray</td><td>Vadgaon</td><td>VJNT</td><td>FYBsc</td><td>2024015400331541</td><td>O+</td><td>patildattatray910@gmail.com</td><td></td><td></td></tr>
                <tr><td>145</td><td>Pawar Sakshi Mukesh</td><td>Tambhole</td><td>OBC</td><td>FYBsc</td><td>2024015400331475</td><td>B+</td><td>sakshimukesh735070@gmail.com</td><td>7822955365</td><td></td></tr>
                <tr><td>146</td><td>Pawar Sanika Sunil</td><td>Dhamangaon</td><td>OBC</td><td>FYBsc</td><td>2024015400331405</td><td>B+</td><td>sunilbalajipawar107@gmail.com</td><td>8010124005</td><td></td></tr>
                <tr><td>147</td><td>Pawar Tushar Sachin</td><td>Shindi</td><td></td><td>FYBsc</td><td>2024015400330131</td><td>B+</td><td>tusharpawar2209@gmail.com</td><td>7620218704</td><td></td></tr>
                <tr><td>148</td><td>Pawar Vishal Ravindra</td><td></td><td></td><td>FYBsc</td><td>2024015400330127</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>149</td><td>Pilore Mahesh Bhausaheb</td><td></td><td></td><td>FYBsc</td><td>2024015400331193</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>150</td><td>Rajput Chetna Bhimsing</td><td>Mehunbare</td><td>DTNT</td><td>FYBsc</td><td>2024015400347652</td><td>B+</td><td>rajputchetna795@gmail.com</td><td>9209749683</td><td></td></tr>
                <tr><td>151</td><td>Rajput Kalyani Nitin</td><td></td><td></td><td>FYBsc</td><td>2024015400336534</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>152</td><td>Rajput Mitali Ravindra</td><td>Chalisgaon</td><td></td><td>FYBsc</td><td>2024015400347362</td><td></td><td>rajashrirajput6@gmail.com</td><td>8888540571</td><td></td></tr>
                <tr><td>153</td><td>Rajput Pradip Subhash</td><td></td><td></td><td>FYBsc</td><td>2024015400351777</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>154</td><td>Rajput Priti Nilesh</td><td></td><td></td><td>FYBsc</td><td>2024015400331185</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>155</td><td>Rajput Sonali Vijay</td><td>Bangaon</td><td>DTNT</td><td>FYBsc</td><td>2024015400330665</td><td></td><td>pardeshibarku@gmail.com</td><td>985070701</td><td></td></tr>
                <tr><td>156</td><td>Rathod Kartik Kalu</td><td></td><td></td><td>FYBsc</td><td>2024015400330634</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>157</td><td>Rathod Nitin Suresh</td><td></td><td></td><td>FYBsc</td><td>2024015400341856</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>158</td><td>Salunkhe Divya Sanjay</td><td>Mahunbare</td><td>OBC</td><td>FYBsc</td><td>2024015400347482</td><td></td><td>divya16csn@gmail.com</td><td>9689962573</td><td></td></tr>
                <tr><td>159</td><td>Salunkhe Supriya Ankush</td><td>Mehunbare</td><td>OBC</td><td>FYBsc</td><td>2024015400341872</td><td>O+</td><td>supriyasalunke7757@gmail.com</td><td>7757860745</td><td></td></tr>
                <tr><td>160</td><td>Savalkar Snehal Nana</td><td>Patonda</td><td>OBC</td><td>FYBsc</td><td>2024015400331394</td><td>B+</td><td>snehalsavarkar98@gmail.com</td><td>9021229275</td><td></td></tr>
                <tr><td>161</td><td>Shaikh Affan Javed</td><td>Bhadgaon</td><td></td><td>FYBsc</td><td>2024015400331982</td><td></td><td>aadfuuzz85658@gmail.com</td><td>8800423551</td><td></td></tr>
                <tr><td>162</td><td>Shaikh Alfiya Shaikh</td><td></td><td></td><td>FYBsc</td><td>2024015400341601</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>163</td><td>Shaikh Aman Aarif</td><td>Chalisgaon</td><td></td><td>FYBsc</td><td>2024015400351804</td><td>B+</td><td>amanshekhcsn@gmail.com</td><td>9579142270</td><td></td></tr>
                <tr><td>164</td><td>Shaikh Arkan Zubair</td><td></td><td></td><td>FYBsc</td><td>2024015400342345</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>165</td><td>Shaikh Farhan Sagir</td><td>Chalisgaon</td><td></td><td>FYBsc</td><td>2024015400331966</td><td>O+</td><td>farhanskar@gmail.com</td><td>9021011203</td><td></td></tr>
                <tr><td>166</td><td>Shaikh Maseera Mazhar</td><td>Chalisgaon</td><td></td><td>FYBsc</td><td>2024015400342384</td><td>A+</td><td>masirashaikhmasina@gmail.com</td><td>7378603033</td><td></td></tr>
                <tr><td>167</td><td>Shaikh Mohammad Affan</td><td></td><td></td><td>FYBsc</td><td>2024015400342233</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>168</td><td>Shaikh Muskan Shakir</td><td></td><td></td><td>FYBsc</td><td>2024015400348953</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>169</td><td>Shinde Sarthak Sunil</td><td></td><td></td><td>FYBsc</td><td>2024015400341887</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>170</td><td>Sonawane Ajay Vijay</td><td></td><td></td><td>FYBsc</td><td>2024015400330673</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>171</td><td>Sonawane Bhushan Vithal</td><td>Tarwade</td><td></td><td>FYBsc</td><td>2024015400330592</td><td></td><td>bhushsankoli792@gmail.com</td><td>9209236908</td><td></td></tr>
                <tr><td>172</td><td>Sonawane Om Ravindra</td><td></td><td></td><td>FYBsc</td><td>2024015400332037</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>173</td><td>Sonawane Yogaraj Kailas</td><td></td><td></td><td>FYBsc</td><td>2024015400351785</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>174</td><td>Suryawanshi Anita Sahebrao</td><td>Wagali</td><td>OBC</td><td>FYBsc</td><td>2024015400347853</td><td>A+</td><td>anitasuryawanshi746@gmail.com</td><td>7249580177</td><td></td></tr>
                <tr><td>175</td><td>Suryawanshi Divya Kiran</td><td>Pimparkheda</td><td>OBC</td><td>FYBsc</td><td>2024015400347717</td><td>B+</td><td>divyasuryawanshi405@gmail.com</td><td>9975628384</td><td></td></tr>
                <tr><td>176</td><td>Suryawanshi Gaurav Pradip</td><td></td><td></td><td>FYBsc</td><td>2024015400347814</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>177</td><td>Suryawanshi Himanshu Ravindra</td><td>Alwadi</td><td>OBC</td><td>FYBsc</td><td>2024015400347733</td><td>B+</td><td>suryawanshihimanshu4488@gmail.com</td><td>7558421217</td><td></td></tr>
                <tr><td>178</td><td>Suryawanshi Jagdish Narendra</td><td></td><td></td><td>FYBsc</td><td>2024015400331943</td><td></td><td></td><td></td><td>15 March 2007</td></tr>
                <tr><td>179</td><td>Suryawanshi Nilesh Suresh</td><td>Ranjangaon</td><td>OBC</td><td>FYBsc</td><td>2024015400342585</td><td>O+</td><td>nusur424@gmail.com</td><td>8600562335</td><td>18 July 2005</td></tr>
                <tr><td>180</td><td>Suryawanshi Nisha Anil</td><td>Pimparkheda</td><td>OBC</td><td>FYBsc</td><td>2024015400331065</td><td>O+</td><td>nishu06049807@gamil.com</td><td>9890405532</td><td></td></tr>
                <tr><td>181</td><td>Thakur Gayatri Gorakh</td><td>Nhave</td><td>ST</td><td>FYBsc</td><td>2024015400347594</td><td>A+</td><td>gorakhnaththakur8@gmail.com</td><td>9834877122</td><td></td></tr>
                <tr><td>182</td><td>Thase Harshada Vishwanath</td><td>Pimparkheda</td><td>OBC</td><td>FYBsc</td><td>2024015400331614</td><td>A+</td><td>harshadathube@gmail.com</td><td>9604544715</td><td></td></tr>
                <tr><td>183</td><td>Thube Ashwini Ravindra</td><td></td><td></td><td>FYBsc</td><td>2024015400347772</td><td></td><td></td><td></td><td></td></tr>
                <tr><td>184</td><td>Upalkar Harshal Anil</td><td>Patonda</td><td>OBC</td><td>FYBsc</td><td>2024015400342063</td><td>O+</td><td>upalkarharshalcsn@gmail.com</td><td>9665201370</td><td>11 March 2006</td></tr>
                <tr><td>185</td><td>Yeole Chaitali Govind</td><td>Ranjangaon</td><td>OBC</td><td>FYBsc</td><td>2024015400350422</td><td>B+</td><td>chaitaliyeole16@gmail.com</td><td>7447462045</td><td></td></tr>
                <tr><td>186</td><td>Zagade Yogesh Sanjay</td><td>Patonda</td><td>OBC</td><td>FYBsc</td><td>2024015400341895</td><td>A+</td><td>yogeshzagade332@gmail.com</td><td>7841871030</td><td></td></tr>
                <tr><td>187</td><td>Zodage Vikas Gorakh</td><td>Rahipuri</td><td>OBC</td><td>FYBsc</td><td>2024015400341582</td><td></td><td>vikaszodage7226@gmail.com</td><td>9359112459</td><td></td></tr>
            </tbody>
        </table>
    </div>

    <script>
        const allStudentsData = [];
        let currentEditingStudentIndex = -1; 

        document.addEventListener('DOMContentLoaded', () => {
            const tableBody = document.getElementById('studentTableBody');
            const rows = tableBody.getElementsByTagName('tr');
            for (let i = 0; i < rows.length; i++) {
                const cells = rows[i].getElementsByTagName('td');
                const student = {
                    srNo: cells[0].textContent || 'N/A',
                    name: cells[1].textContent || 'N/A',
                    address: cells[2].textContent || 'N/A',
                    category: cells[3].textContent || 'N/A',
                    className: cells[4].textContent || 'N/A',
                    prnNo: cells[5].textContent || 'N/A',
                    bloodGroup: cells[6].textContent || 'N/A',
                    emailId: cells[7].textContent ? cells[7].textContent.toLowerCase() : 'N/A',
                    mobileNo: cells[8].textContent || 'N/A',
                    dob: cells[9].textContent || 'N/A',
                };
                allStudentsData.push(student);
                rows[i].setAttribute('data-student-index', i);
                // टेबलमधील रो (<tr>) वर क्लिक केल्यास प्रोफाइल उघडेल.
                rows[i].addEventListener('click', () => displayStudentProfile(i));
            }
            
            // फक्त डीबगिंगसाठी: कन्सोलमध्ये allStudentsData तपासा.
            // Console (F12) उघडून 'allStudentsData' असे टाइप करून Enter दाबा.
            // जर हा ॲरे रिकामा नसेल, तर याचा अर्थ डेटा योग्यरित्या पॉप्युलेट झाला आहे.
            console.log('allStudentsData populated:', allStudentsData.length, 'students');

            const searchResultsDiv = document.getElementById('searchResults');
            searchResultsDiv.classList.remove('visible'); 
            searchResultsDiv.innerHTML = ''; 

            const studentProfileDiv = document.getElementById('studentProfile');
            studentProfileDiv.classList.remove('visible');
            studentProfileDiv.innerHTML = '<h3>Select a Student</h3><p>Click on a student from the search results or the list below to view their details.</p>';
        });

        function handleSearchInput(event) {
            const input = document.getElementById('studentNameInput').value.toLowerCase().trim();
            const searchResultsDiv = document.getElementById('searchResults');
            const studentProfileDiv = document.getElementById('studentProfile');

            if (event.keyCode === 13 || event.key === 'Enter') {
                searchStudent();
            } else {
                if (input === "") {
                    searchResultsDiv.classList.remove('visible'); 
                    searchResultsDiv.innerHTML = ''; 
                    
                    studentProfileDiv.classList.remove('visible');
                    studentProfileDiv.innerHTML = '<h3>Select a Student</h3><p>Click on a student from the search results or the list below to view their details.</p>';
                } 
            }
        }

        function searchStudent() {
            const input = document.getElementById('studentNameInput').value.toLowerCase().trim();
            const searchResultsDiv = document.getElementById('searchResults');
            const studentProfileDiv = document.getElementById('studentProfile');
            
            studentProfileDiv.classList.remove('visible'); 
            currentEditingStudentIndex = -1;

            if (input === "") {
                searchResultsDiv.classList.remove('visible');
                searchResultsDiv.innerHTML = ''; 
                return; 
            }

            let resultsHtml = '<h3>Search Results</h3>';
            const matchingStudents = [];

            for (let i = 0; i < allStudentsData.length; i++) {
                const student = allStudentsData[i];
                if (
                    student.name.toLowerCase().includes(input) ||
                    student.address.toLowerCase().includes(input) ||
                    student.prnNo.toLowerCase().includes(input) ||
                    student.emailId.toLowerCase().includes(input) || 
                    student.mobileNo.includes(input) 
                ) {
                    matchingStudents.push({student: student, index: i});
                }
            }

            if (matchingStudents.length > 0) {
                if (matchingStudents.length === 1 && input === matchingStudents[0].student.name.toLowerCase()) {
                    displayStudentProfile(matchingStudents[0].index); // इथे थेट प्रोफाइल दाखवले जाते
                    searchResultsDiv.classList.remove('visible'); // सर्च रिझल्ट्स लपवले जातात
                    searchResultsDiv.innerHTML = ''; 
                } else {
                    resultsHtml += '<ul>';
                    matchingStudents.forEach((item) => {
                        // सर्च रिझल्ट्समधील नावावर (<li>) क्लिक केल्यास प्रोफाइल उघडेल.
                        resultsHtml += `<li onclick="displayStudentProfile(${item.index})">${item.student.name} (${item.student.prnNo})</li>`;
                    });
                    resultsHtml += '</ul>';
                    searchResultsDiv.innerHTML = resultsHtml;
                    searchResultsDiv.classList.add('visible'); 
                }
            } else {
                searchResultsDiv.innerHTML = '<h3>Search Results</h3><p>No information found. Please check the full name, PRN number, address, email, or mobile number.</p>';
                searchResultsDiv.classList.add('visible'); 
            }
        }

        function displayStudentProfile(studentIndex) {
            console.log('displayStudentProfile called with index:', studentIndex);

            const student = allStudentsData[studentIndex];
            currentEditingStudentIndex = studentIndex;
            const studentProfileDiv = document.getElementById('studentProfile');
            const searchResultsDiv = document.getElementById('searchResults'); 

            if (student) {
                console.log('Student data found:', student.name); 
                let profileHtml = '<h3>Complete Student Information:</h3>';
                profileHtml += '<div class="profile-field"><strong>SR.No.:</strong> <span id="profile-srNo">' + student.srNo + '</span></div>';
                profileHtml += '<div class="profile-field"><strong>Name:</strong> <span id="profile-name">' + student.name + '</span></div>';
                profileHtml += '<div class="profile-field"><strong>Address:</strong> <span id="profile-address">' + student.address + '</span></div>';
                profileHtml += '<div class="profile-field"><strong>Category:</strong> <span id="profile-category">' + student.category + '</span></div>';
                profileHtml += '<div class="profile-field"><strong>Class:</strong> <span id="profile-className">' + student.className + '</span></div>';
                profileHtml += '<div class="profile-field"><strong>PRN No.:</strong> <span id="profile-prnNo">' + student.prnNo + '</span></div>';
                profileHtml += '<div class="profile-field"><strong>Blood Group:</strong> <span id="profile-bloodGroup">' + student.bloodGroup + '</span></div>';
                profileHtml += '<div class="profile-field"><strong>Email ID:</strong> <span id="profile-emailId">' + student.emailId + '</span></div>';
                profileHtml += '<div class="profile-field"><strong>Mobile No.:</strong> <span id="profile-mobileNo">' + student.mobileNo + '</span></div>';
                profileHtml += '<div class="profile-field"><strong>Date of Birth:</strong> <span id="profile-dob">' + student.dob + '</span></div>';
                
                profileHtml += '<div class="profile-actions">';
                profileHtml += '<button id="closeProfileBtn" class="close-btn" onclick="closeStudentProfile()">Close</button>';
                profileHtml += '</div>';
                
                studentProfileDiv.innerHTML = profileHtml;
                studentProfileDiv.classList.add('visible'); // प्रोफाइलला दृश्यमान (visible) करते
                
                // *** ही नवीन ओळ जोडली आहे ज्यामुळे प्रोफाइल स्क्रीनवर दिसेल ***
                studentProfileDiv.scrollIntoView({ behavior: 'smooth', block: 'start' }); 

                searchResultsDiv.classList.remove('visible'); // सर्च रिझल्ट्स लपवते
                searchResultsDiv.innerHTML = ''; 
            } else {
                console.log('Student data not found for index:', studentIndex); 
                studentProfileDiv.innerHTML = '<h3>Select a Student</h3><p>Information not available.</p>';
                studentProfileDiv.classList.remove('visible'); 
            }
        }
        
        function closeStudentProfile() {
            const studentProfileDiv = document.getElementById('studentProfile');
            studentProfileDiv.classList.remove('visible');
            studentProfileDiv.innerHTML = '<h3>Select a Student</h3><p>Click on a student from the search results or the list below to view their details.</p>';
            currentEditingStudentIndex = -1;
        }

    </script>

</body>
</html>
