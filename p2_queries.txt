USE LibraryManagement;

-- Insert mock authors
INSERT INTO authors (author_name) VALUES 
	('Taras Shevchenko'), 
    ('Maks Kidruk'), 
    ('Serhii Plokhy');

-- Create mock genres
INSERT INTO genres (genre_name) VALUES
	('Historical Fiction'),
	('Science Fiction'),
	('Biography'),
	('Mystery'),
	('Fantasy');
    SHOW CREATE TABLE books;
    
-- Insert mock data into books table
INSERT INTO books (title, publication_year, author_id, genre_id) VALUES
	('Kobzar', 1840, 1, 1),  -- Taras Shevchenko, Historical Fiction
	('Bot', 2012, 2, 2),  -- Maks Kidruk, Sci-Fi
	('The Last Empire', 2014, 3, 3),  -- Serhii Plokhy, Biography
	('Zhora', 2019, 2, 2),  -- Maks Kidruk, Sci-Fi
	('Chernobyl: The History of a Nuclear Catastrophe', 2018, 3, 3);  -- Serhii Plokhy, Biography
    
-- Insert mock data into users table
INSERT INTO users (username, email) VALUES
	('booklover21', 'booklover21@example.com'),
	('historybuff', 'historybuff@example.com'),
	('scififan99', 'scififan99@example.com'),
	('mysteryreader', 'mysteryreader@example.com'),
	('fantasygeek', 'fantasygeek@example.com');

-- Insert mock data into borrowed_books table
INSERT INTO borrowed_books (book_id, user_id, borrow_date, return_date) VALUES
	(1, 1, '2024-01-10', '2024-02-05'),  -- Kobzar borrowed by booklover21
	(2, 2, '2024-01-15', NULL),  -- Bot borrowed by historybuff (still borrowed)
	(3, 3, '2024-02-01', '2024-02-20'),  -- The Last Empire borrowed by scififan99
	(4, 4, '2024-02-10', NULL),  -- Zhora borrowed by mysteryreader (still borrowed)
	(5, 5, '2024-02-15', '2024-03-01');  -- Chernobyl: The History borrowed by fantasygeek