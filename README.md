1️⃣ Création des tables

-- Table des ventes
CREATE TABLE ventes (
    id SERIAL PRIMARY KEY,
    date_vente DATE NOT NULL,
    client VARCHAR(50),
    mode_paiement VARCHAR(30),
    montant_vente INT,
    description TEXT,
    montant_depense INT,
    categorie VARCHAR(30)
);

2️⃣ Insertion des données

INSERT INTO ventes (date_vente, client, mode_paiement, montant_vente, description, montant_depense, categorie)
VALUES
('2021-01-10', 'Moussa Diallo', 'Weave', 375000, 'payé les Frais de Livraison Payer et à rembourser une fois le produit arrivé', 455, 'Exportation'),
('2020-03-10', 'Moussa Diallo', 'Orange Money', 600000, 'payé les Frais de Livraison Payer et à rembourser une fois le produit arrivé', 35, 'Livraison Local'),
('2020-01-10', 'Fatou Sall', 'Carte Visa', 750000, 'payé les Frais de Livraison Payer et à rembourser une fois le produit arrivé', 400, 'Exportation'),
('2021-01-10', 'Ibrahim Koné', 'Orange Money', 1225000, 'payé les Frais de Livraison Payer et à rembourser une fois le produit arrivé', 350, 'Exportation'),
('2020-01-10', 'Aminata Traoré', 'Carte Visa', 800000, 'payé les Frais de Livraison Payer et à rembourser une fois le produit arrivé', 353, 'Livraison Local'),
('2020-01-10', 'Cheikh Ba', 'Carte Visa', 150000, 'payé les Frais de Livraison Payer et à rembourser une fois le produit arrivé', 350, 'Exportation'),
('2021-01-10', 'Aminata Traoré', 'Weave', 2475000, 'payé les Frais de Livraison Payer et à rembourser une fois le produit arrivé', 4500, 'Livraison Local'),
('2020-01-10', 'Moussa Diallo', 'Orange Money', 500000, 'remboursement des 200k à la banque + frais de 2000FCFA', 3000, 'Exportation'),
('2020-01-10', 'Cheikh Ba', 'Carte Visa', 135000, 'payé les Frais de Livraison Payer et à rembourser une fois le produit arrivé', 3450, 'Exportation'),
('2021-01-10', 'Fatou Sall', 'Carte Visa', 875000, 'payé les Frais de Livraison Payer et à rembourser une fois le produit arrivé', 455, 'Livraison Local');

3️⃣ Requêtes d’analyse
🔹 Chiffre d’affaires total

SELECT SUM(montant_vente) AS total_ventes FROM ventes;

Dépenses totales

SELECT SUM(montant_depense) AS total_depenses FROM ventes;

Bénéfices

SELECT SUM(montant_vente - montant_depense) AS total_benefices FROM ventes;

Répartition par catégorie

SELECT categorie, SUM(montant_vente) AS ventes_par_categorie
FROM ventes
GROUP BY categorie;
Répartition par mode de paiement

SELECT mode_paiement, COUNT(*) AS nombre_transactions, SUM(montant_vente) AS total_ventes
FROM ventes
GROUP BY mode_paiement;

Bénéfices par client
sql
SELECT client, SUM(montant_vente - montant_depense) AS benefice_client
FROM ventes
GROUP BY client
ORDER BY benefice_client DESC;
4️⃣ Vue pour Power BI / Excel
CREATE VIEW vue_dashboard AS
SELECT
    date_vente,
    client,
    mode_paiement,
    categorie,
    montant_vente,
    montant_depense,
    (montant_vente - montant_depense) AS benefice
FROM ventes;
-- Vérifier les ventes par année
SELECT EXTRACT(YEAR FROM date_vente) AS annee, SUM(montant_vente) AS total_ventes
FROM ventes
GROUP BY annee
ORDER BY annee;
