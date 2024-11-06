-- Poistetaan vanha tietokanta ja luodaan uusi
DROP DATABASE IF EXISTS mediashare;
CREATE DATABASE mediashare;
USE mediashare;

-- Taulu: Users
CREATE TABLE Users (
  user_id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
  username VARCHAR(255) NOT NULL UNIQUE,
  password VARCHAR(255) NOT NULL,
  email VARCHAR(255) NOT NULL UNIQUE,
  user_level_id INT NOT NULL,
  created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP
);

-- Taulu: MediaItems
CREATE TABLE MediaItems (
  media_id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
  user_id INT NOT NULL,
  filename VARCHAR(255) NOT NULL,
  filesize INT NOT NULL,
  media_type VARCHAR(255) NOT NULL,
  title VARCHAR(255) NOT NULL,
  description VARCHAR(255),
  created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (user_id) REFERENCES Users(user_id)
);

-- Taulu: Products
CREATE TABLE Products (
  product_id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
  media_id INT NOT NULL,
  name VARCHAR(255) NOT NULL,
  price DECIMAL(10, 2) NOT NULL,
  discount DECIMAL(5, 2) DEFAULT 0.00,
  description TEXT,
  image_urls TEXT,
  created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (media_id) REFERENCES MediaItems(media_id)
);

-- Taulu: Feedback
CREATE TABLE Feedback (
  feedback_id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
  media_id INT NOT NULL,
  user_id INT NOT NULL,
  name VARCHAR(255) NOT NULL,
  email VARCHAR(255) NOT NULL,
  message TEXT NOT NULL,
  created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (media_id) REFERENCES MediaItems(media_id),
  FOREIGN KEY (user_id) REFERENCES Users(user_id)
);

-- Esimerkkitietojen lisääminen Users-tauluun
INSERT INTO Users (username, password, email, user_level_id) VALUES 
  ('VCHar', 'salasana123', 'vchar@example.com', 1),
  ('Donatello', 'salasana234', 'dona@example.com', 1);

-- Esimerkkitietojen lisääminen MediaItems-tauluun
INSERT INTO MediaItems (filename, filesize, title, description, user_id, media_type) VALUES 
  ('ffd8.jpg', 887574, 'Lempijuoma', NULL, 305, 'image/jpeg'),
  ('dbbd.jpg', 60703, 'Miika', 'Oma kuva', 305, 'image/jpeg');

-- Esimerkkitietojen lisääminen Products-tauluun
INSERT INTO Products (media_id, name, price, discount, description, image_urls) VALUES 
  (1, 'Tuote A', 19.99, 2.00, 'Esimerkkituotteen kuvaus Tuote A:lle.', 'kuvaA.jpg'),
  (2, 'Tuote B', 29.99, 0.00, 'Kuvaus Tuote B:lle, laadukas tuote.', 'kuvaB.jpg');

-- Esimerkkitietojen lisääminen Feedback-tauluun
INSERT INTO Feedback (media_id, user_id, name, email, message) VALUES 
  (1, 305, 'John Doe', 'john.doe@example.com', 'Mahtavia tuotteita! Olen erittäin tyytyväinen.'),
  (2, 260, 'Jane Smith', 'jane.smith@example.com', 'Asiakastuki oli erittäin avulias!'),
  (1, 260, 'Alice Johnson', 'alice.johnson@example.com', 'Toimitus oli nopea ja tuotteet olivat kuvauksen mukaisia.');

-- Kyselyt esimerkkikäyttötilanteisiin

-- Hae kaikki palautteet tietylle medialle (esim. media_id = 1)
SELECT * FROM Feedback WHERE media_id = 1;

-- Hae tietyn käyttäjän kaikki media-tiedostot (esim. user_id = 305)
SELECT * FROM MediaItems WHERE user_id = 305;

-- Hae kaikki tuotteet, joilla on alennus
SELECT * FROM Products WHERE discount > 0;

-- Päivitä esimerkkikäyttötilanteessa tietyn tuotteen hinta
UPDATE Products
SET price = 24.99
WHERE product_id = 1;

-- Poista esimerkkikäyttötilanteessa tietty palaute (esim. feedback_id = 1)
DELETE FROM Feedback
WHERE feedback_id = 1;
