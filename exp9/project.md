I'll create a simple web application for the Department of Artificial Intelligence and Data Science. Here's a complete implementation:

## Directory Structure
```
ai-department/
├── index.php
├── style.css
├── about.php
├── courses.php
├── faculty.php
└── contact.php
```

## 1. index.php (Main Page)
```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Department of AI & Data Science</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <!-- Header -->
    <header>
        <nav class="navbar">
            <div class="nav-container">
                <h1 class="logo">AI & Data Science</h1>
                <ul class="nav-menu">
                    <li><a href="index.php" class="nav-link active">Home</a></li>
                    <li><a href="about.php" class="nav-link">About</a></li>
                    <li><a href="courses.php" class="nav-link">Courses</a></li>
                    <li><a href="faculty.php" class="nav-link">Faculty</a></li>
                    <li><a href="contact.php" class="nav-link">Contact</a></li>
                </ul>
            </div>
        </nav>
    </header>

    <!-- Hero Section -->
    <section class="hero">
        <div class="hero-content">
            <h2>Welcome to the Department of</h2>
            <h1>Artificial Intelligence & Data Science</h1>
            <p>Shaping the future through intelligent systems and data-driven insights</p>
            <a href="about.php" class="cta-button">Learn More</a>
        </div>
    </section>

    <!-- Features Section -->
    <section class="features">
        <div class="container">
            <h2>Why Choose Our Department?</h2>
            <div class="features-grid">
                <div class="feature-card">
                    <h3>Cutting-edge Research</h3>
                    <p>Engage in groundbreaking research in AI, ML, and data analytics</p>
                </div>
                <div class="feature-card">
                    <h3>Industry Partnerships</h3>
                    <p>Collaborate with leading tech companies and research institutions</p>
                </div>
                <div class="feature-card">
                    <h3>Expert Faculty</h3>
                    <p>Learn from experienced professionals and researchers</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Latest News -->
    <section class="news">
        <div class="container">
            <h2>Latest News</h2>
            <div class="news-grid">
                <?php
                // Sample news data - in real application, this would come from database
                $news_items = [
                    [
                        'title' => 'New Research Lab Inaugurated',
                        'date' => '2024-01-15',
                        'excerpt' => 'State-of-the-art AI research laboratory opened with advanced computing resources.'
                    ],
                    [
                        'title' => 'Industry Collaboration Program',
                        'date' => '2024-01-10',
                        'excerpt' => 'Partnership with leading tech companies for student internships and projects.'
                    ],
                    [
                        'title' => 'International Conference 2024',
                        'date' => '2024-01-05',
                        'excerpt' => 'Call for papers announced for our annual international AI conference.'
                    ]
                ];

                foreach ($news_items as $news) {
                    echo "
                    <div class='news-card'>
                        <h3>{$news['title']}</h3>
                        <span class='news-date'>{$news['date']}</span>
                        <p>{$news['excerpt']}</p>
                    </div>
                    ";
                }
                ?>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer>
        <div class="container">
            <p>&copy; 2024 Department of Artificial Intelligence & Data Science. All rights reserved.</p>
        </div>
    </footer>
</body>
</html>
```

## 2. style.css
```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: 'Arial', sans-serif;
    line-height: 1.6;
    color: #333;
}

.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
}

/* Header & Navigation */
.navbar {
    background: #2c3e50;
    padding: 1rem 0;
    position: fixed;
    width: 100%;
    top: 0;
    z-index: 1000;
}

.nav-container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.logo {
    color: white;
    font-size: 1.8rem;
    font-weight: bold;
}

.nav-menu {
    display: flex;
    list-style: none;
    gap: 2rem;
}

.nav-link {
    color: white;
    text-decoration: none;
    transition: color 0.3s;
}

.nav-link:hover,
.nav-link.active {
    color: #3498db;
}

/* Hero Section */
.hero {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    padding: 150px 0 100px;
    text-align: center;
}

.hero-content h1 {
    font-size: 3rem;
    margin-bottom: 1rem;
}

.hero-content h2 {
    font-size: 1.5rem;
    margin-bottom: 1rem;
    opacity: 0.9;
}

.hero-content p {
    font-size: 1.2rem;
    margin-bottom: 2rem;
    opacity: 0.8;
}

.cta-button {
    display: inline-block;
    background: #e74c3c;
    color: white;
    padding: 12px 30px;
    text-decoration: none;
    border-radius: 5px;
    transition: background 0.3s;
}

.cta-button:hover {
    background: #c0392b;
}

/* Features Section */
.features {
    padding: 80px 0;
    background: #f8f9fa;
}

.features h2 {
    text-align: center;
    margin-bottom: 3rem;
    font-size: 2.5rem;
    color: #2c3e50;
}

.features-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
}

.feature-card {
    background: white;
    padding: 2rem;
    border-radius: 10px;
    box-shadow: 0 5px 15px rgba(0,0,0,0.1);
    text-align: center;
    transition: transform 0.3s;
}

.feature-card:hover {
    transform: translateY(-5px);
}

.feature-card h3 {
    color: #2c3e50;
    margin-bottom: 1rem;
}

/* News Section */
.news {
    padding: 80px 0;
}

.news h2 {
    text-align: center;
    margin-bottom: 3rem;
    font-size: 2.5rem;
    color: #2c3e50;
}

.news-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
    gap: 2rem;
}

.news-card {
    background: white;
    padding: 2rem;
    border-radius: 10px;
    box-shadow: 0 5px 15px rgba(0,0,0,0.1);
    border-left: 4px solid #3498db;
}

.news-card h3 {
    color: #2c3e50;
    margin-bottom: 0.5rem;
}

.news-date {
    color: #7f8c8d;
    font-size: 0.9rem;
    margin-bottom: 1rem;
    display: block;
}

/* Footer */
footer {
    background: #2c3e50;
    color: white;
    text-align: center;
    padding: 2rem 0;
}

/* Responsive Design */
@media (max-width: 768px) {
    .nav-menu {
        flex-direction: column;
        gap: 1rem;
    }
    
    .hero-content h1 {
        font-size: 2rem;
    }
    
    .hero-content h2 {
        font-size: 1.2rem;
    }
}
```

## 3. about.php
```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>About - AI & Data Science Department</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header>
        <nav class="navbar">
            <div class="nav-container">
                <h1 class="logo">AI & Data Science</h1>
                <ul class="nav-menu">
                    <li><a href="index.php" class="nav-link">Home</a></li>
                    <li><a href="about.php" class="nav-link active">About</a></li>
                    <li><a href="courses.php" class="nav-link">Courses</a></li>
                    <li><a href="faculty.php" class="nav-link">Faculty</a></li>
                    <li><a href="contact.php" class="nav-link">Contact</a></li>
                </ul>
            </div>
        </nav>
    </header>

    <section class="hero" style="padding: 120px 0 80px; background: linear-gradient(135deg, #3498db 0%, #2c3e50 100%);">
        <div class="container">
            <h1>About Our Department</h1>
        </div>
    </section>

    <section class="features" style="padding: 60px 0;">
        <div class="container">
            <div class="about-content">
                <h2>Our Mission</h2>
                <p>To advance the frontiers of Artificial Intelligence and Data Science through innovative research, quality education, and meaningful industry collaborations.</p>
                
                <h2>Vision</h2>
                <p>To be a globally recognized center of excellence in AI and Data Science education and research, producing leaders who drive technological innovation.</p>
                
                <h2>Programs Offered</h2>
                <ul>
                    <li>B.Tech in Artificial Intelligence and Data Science</li>
                    <li>M.Tech in Artificial Intelligence</li>
                    <li>M.Tech in Data Science</li>
                    <li>Ph.D. in AI and Data Science</li>
                </ul>
            </div>
        </div>
    </section>

    <footer>
        <div class="container">
            <p>&copy; 2024 Department of Artificial Intelligence & Data Science. All rights reserved.</p>
        </div>
    </footer>
</body>
</html>
```

## 4. courses.php
```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Courses - AI & Data Science Department</title>
    <link rel="stylesheet" href="style.css">
    <style>
        .courses-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2rem;
            margin-top: 2rem;
        }
        
        .course-card {
            background: white;
            padding: 2rem;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            border-top: 4px solid #3498db;
        }
        
        .course-card h3 {
            color: #2c3e50;
            margin-bottom: 1rem;
        }
        
        .course-code {
            color: #7f8c8d;
            font-weight: bold;
            margin-bottom: 1rem;
            display: block;
        }
    </style>
</head>
<body>
    <header>
        <nav class="navbar">
            <div class="nav-container">
                <h1 class="logo">AI & Data Science</h1>
                <ul class="nav-menu">
                    <li><a href="index.php" class="nav-link">Home</a></li>
                    <li><a href="about.php" class="nav-link">About</a></li>
                    <li><a href="courses.php" class="nav-link active">Courses</a></li>
                    <li><a href="faculty.php" class="nav-link">Faculty</a></li>
                    <li><a href="contact.php" class="nav-link">Contact</a></li>
                </ul>
            </div>
        </nav>
    </header>

    <section class="hero" style="padding: 120px 0 80px; background: linear-gradient(135deg, #9b59b6 0%, #3498db 100%);">
        <div class="container">
            <h1>Our Courses</h1>
            <p>Comprehensive curriculum covering all aspects of AI and Data Science</p>
        </div>
    </section>

    <section class="features" style="padding: 60px 0;">
        <div class="container">
            <h2>Undergraduate Courses</h2>
            <div class="courses-grid">
                <?php
                $ug_courses = [
                    ['code' => 'AIDS101', 'name' => 'Introduction to Artificial Intelligence', 'credits' => 4],
                    ['code' => 'AIDS102', 'name' => 'Programming for Data Science', 'credits' => 4],
                    ['code' => 'AIDS201', 'name' => 'Machine Learning Fundamentals', 'credits' => 4],
                    ['code' => 'AIDS202', 'name' => 'Data Structures and Algorithms', 'credits' => 4],
                    ['code' => 'AIDS301', 'name' => 'Deep Learning', 'credits' => 4],
                    ['code' => 'AIDS302', 'name' => 'Big Data Analytics', 'credits' => 4],
                ];
                
                foreach ($ug_courses as $course) {
                    echo "
                    <div class='course-card'>
                        <span class='course-code'>{$course['code']} - {$course['credits']} Credits</span>
                        <h3>{$course['name']}</h3>
                    </div>
                    ";
                }
                ?>
            </div>
            
            <h2 style="margin-top: 4rem;">Postgraduate Courses</h2>
            <div class="courses-grid">
                <?php
                $pg_courses = [
                    ['code' => 'AIDS501', 'name' => 'Advanced Machine Learning', 'credits' => 4],
                    ['code' => 'AIDS502', 'name' => 'Natural Language Processing', 'credits' => 4],
                    ['code' => 'AIDS503', 'name' => 'Computer Vision', 'credits' => 4],
                    ['code' => 'AIDS504', 'name' => 'Reinforcement Learning', 'credits' => 4],
                ];
                
                foreach ($pg_courses as $course) {
                    echo "
                    <div class='course-card'>
                        <span class='course-code'>{$course['code']} - {$course['credits']} Credits</span>
                        <h3>{$course['name']}</h3>
                    </div>
                    ";
                }
                ?>
            </div>
        </div>
    </section>

    <footer>
        <div class="container">
            <p>&copy; 2024 Department of Artificial Intelligence & Data Science. All rights reserved.</p>
        </div>
    </footer>
</body>
</html>
```

## 5. faculty.php
```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Faculty - AI & Data Science Department</title>
    <link rel="stylesheet" href="style.css">
    <style>
        .faculty-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2rem;
            margin-top: 2rem;
        }
        
        .faculty-card {
            background: white;
            padding: 2rem;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            text-align: center;
        }
        
        .faculty-img {
            width: 150px;
            height: 150px;
            border-radius: 50%;
            margin: 0 auto 1rem;
            background: #3498db;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 3rem;
        }
        
        .faculty-card h3 {
            color: #2c3e50;
            margin-bottom: 0.5rem;
        }
        
        .faculty-role {
            color: #e74c3c;
            font-weight: bold;
            margin-bottom: 1rem;
        }
        
        .faculty-expertise {
            color: #7f8c8d;
            font-style: italic;
        }
    </style>
</head>
<body>
    <header>
        <nav class="navbar">
            <div class="nav-container">
                <h1 class="logo">AI & Data Science</h1>
                <ul class="nav-menu">
                    <li><a href="index.php" class="nav-link">Home</a></li>
                    <li><a href="about.php" class="nav-link">About</a></li>
                    <li><a href="courses.php" class="nav-link">Courses</a></li>
                    <li><a href="faculty.php" class="nav-link active">Faculty</a></li>
                    <li><a href="contact.php" class="nav-link">Contact</a></li>
                </ul>
            </div>
        </nav>
    </header>

    <section class="hero" style="padding: 120px 0 80px; background: linear-gradient(135deg, #e74c3c 0%, #c0392b 100%);">
        <div class="container">
            <h1>Our Faculty</h1>
            <p>Meet our distinguished faculty members</p>
        </div>
    </section>

    <section class="features" style="padding: 60px 0;">
        <div class="container">
            <div class="faculty-grid">
                <?php
                $faculty_members = [
                    [
                        'name' => 'Bruce wayne',
                        'role' => 'Professor & Head of Department',
                        'expertise' => 'Machine Learning, Natural Language Processing'
                    ],
                    [
                        'name' => 'Dr. Jin sakai',
                        'role' => 'Associate Professor',
                        'expertise' => 'Computer Vision, Deep Learning'
                    ],
                    [
                        'name' => 'Dr. Sample kumar',
                        'role' => 'Assistant Professor',
                        'expertise' => 'Data Mining, Big Data Analytics'
                    ],
                    [
                        'name' => 'Dr. idk',
                        'role' => 'Professor',
                        'expertise' => 'Reinforcement Learning, Robotics'
                    ],
                    [
                        'name' => 'Dr. luffy',
                        'role' => 'Associate Professor',
                        'expertise' => 'Statistical Learning, Optimization'
                    ],
                    [
                        'name' => 'Dr. who',
                        'role' => 'Assistant Professor',
                        'expertise' => 'AI Ethics, Explainable AI'
                    ]
                ];
                
                foreach ($faculty_members as $faculty) {
                    $initial = substr($faculty['name'], 0, 1);
                    echo "
                    <div class='faculty-card'>
                        <div class='faculty-img'>$initial</div>
                        <h3>{$faculty['name']}</h3>
                        <div class='faculty-role'>{$faculty['role']}</div>
                        <div class='faculty-expertise'>{$faculty['expertise']}</div>
                    </div>
                    ";
                }
                ?>
            </div>
        </div>
    </section>

    <footer>
        <div class="container">
            <p>&copy; 2024 Department of Artificial Intelligence & Data Science. All rights reserved.</p>
        </div>
    </footer>
</body>
</html>
```

## 6. contact.php
```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Contact - AI & Data Science Department</title>
    <link rel="stylesheet" href="style.css">
    <style>
        .contact-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 3rem;
            margin-top: 2rem;
        }
        
        .contact-info {
            background: white;
            padding: 2rem;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .contact-form {
            background: white;
            padding: 2rem;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .form-group {
            margin-bottom: 1.5rem;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: bold;
            color: #2c3e50;
        }
        
        .form-group input,
        .form-group textarea,
        .form-group select {
            width: 100%;
            padding: 0.8rem;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 1rem;
        }
        
        .form-group textarea {
            height: 120px;
            resize: vertical;
        }
        
        .submit-btn {
            background: #3498db;
            color: white;
            padding: 12px 30px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 1rem;
            transition: background 0.3s;
        }
        
        .submit-btn:hover {
            background: #2980b9;
        }
        
        .info-item {
            margin-bottom: 1.5rem;
            padding-bottom: 1rem;
            border-bottom: 1px solid #ecf0f1;
        }
        
        .info-item h3 {
            color: #2c3e50;
            margin-bottom: 0.5rem;
        }
    </style>
</head>
<body>
    <header>
        <nav class="navbar">
            <div class="nav-container">
                <h1 class="logo">AI & Data Science</h1>
                <ul class="nav-menu">
                    <li><a href="index.php" class="nav-link">Home</a></li>
                    <li><a href="about.php" class="nav-link">About</a></li>
                    <li><a href="courses.php" class="nav-link">Courses</a></li>
                    <li><a href="faculty.php" class="nav-link">Faculty</a></li>
                    <li><a href="contact.php" class="nav-link active">Contact</a></li>
                </ul>
            </div>
        </nav>
    </header>

    <section class="hero" style="padding: 120px 0 80px; background: linear-gradient(135deg, #f39c12 0%, #e67e22 100%);">
        <div class="container">
            <h1>Contact Us</h1>
            <p>Get in touch with our department</p>
        </div>
    </section>

    <section class="features" style="padding: 60px 0;">
        <div class="container">
            <div class="contact-container">
                <div class="contact-info">
                    <h2>Department Information</h2>
                    <div class="info-item">
                        <h3>Address</h3>
                        <p>Department of Artificial Intelligence & Data Science<br>
                           Tech University Campus<br>
                           Innovation Road, Tech City - 560001</p>
                    </div>
                    <div class="info-item">
                        <h3>Contact Details</h3>
                        <p>Phone: +91-80-2658-1234<br>
                           Email: ai.department@techuniv.edu<br>
                           Fax: +91-80-2658-5678</p>
                    </div>
                    <div class="info-item">
                        <h3>Office Hours</h3>
                        <p>Monday - Friday: 9:00 AM - 5:00 PM<br>
                           Saturday: 9:00 AM - 1:00 PM<br>
                           Sunday: Closed</p>
                    </div>
                </div>
                
                <div class="contact-form">
                    <h2>Send us a Message</h2>
                    <form action="" method="POST">
                        <div class="form-group">
                            <label for="name">Full Name</label>
                            <input type="text" id="name" name="name" required>
                        </div>
                        <div class="form-group">
                            <label for="email">Email Address</label>
                            <input type="email" id="email" name="email" required>
                        </div>
                        <div class="form-group">
                            <label for="subject">Subject</label>
                            <select id="subject" name="subject" required>
                                <option value="">Select a subject</option>
                                <option value="admission">Admission Inquiry</option>
                                <option value="course">Course Information</option>
                                <option value="research">Research Collaboration</option>
                                <option value="other">Other</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label for="message">Message</label>
                            <textarea id="message" name="message" required></textarea>
                        </div>
                        <button type="submit" class="submit-btn">Send Message</button>
                    </form>
                    
                    <?php
                    if ($_SERVER["REQUEST_METHOD"] == "POST") {
                        // Basic form processing
                        $name = htmlspecialchars($_POST['name']);
                        $email = htmlspecialchars($_POST['email']);
                        $subject = htmlspecialchars($_POST['subject']);
                        $message = htmlspecialchars($_POST['message']);
                        
                        echo "<div style='margin-top: 1rem; padding: 1rem; background: #d4edda; color: #155724; border-radius: 5px;'>
                                Thank you, $name! Your message has been received. We'll get back to you soon.
                              </div>";
                    }
                    ?>
                </div>
            </div>
        </div>
    </section>

    <footer>
        <div class="container">
            <p>&copy; 2024 Department of Artificial Intelligence & Data Science. All rights reserved.</p>
        </div>
    </footer>
</body>
</html>
```

## Features of this Web Application:

1. **Responsive Design**: Works on all devices
2. **Modern UI**: Clean and professional interface
3. **Navigation**: Easy navigation between pages
4. **Dynamic Content**: PHP-powered content generation
5. **Contact Form**: Functional contact form with basic processing
6. **Multiple Pages**: Home, About, Courses, Faculty, and Contact pages

## How to Run:

1. Create a folder named `ai-department` in your web server directory (like `htdocs` for XAMPP)
2. Save all the files in this folder
3. Start your web server (Apache)
4. Open browser and navigate to `http://localhost/ai-department/`

The application is ready to use and can be extended with database integration, user authentication, and more advanced features as needed.
