-- Adminer 4.7.9 MySQL dump

SET NAMES utf8;
SET time_zone = '+00:00';
SET foreign_key_checks = 0;
SET sql_mode = 'NO_AUTO_VALUE_ON_ZERO';

SET NAMES utf8mb4;

INSERT INTO `Etat` (`id`, `libelle`) VALUES
('12',	'aaa'),
('CL',	'Saisie clôturée'),
('CR',	'Fiche créée, saisie en cours'),
('RB',	'Remboursée'),
('VA',	'Validée et mise en paiements');

INSERT INTO `FicheFrais` (`idVisiteur`, `mois`, `nbJustificatifs`, `montantValide`, `dateModif`, `idEtat`) VALUES
('a131',	'01',	0,	0.00,	'2023-01-26',	'CR');

INSERT INTO `FraisForfait` (`id`, `libelle`, `montant`) VALUES
('ETP',	'Forfait Etape',	110.00),
('KM',	'Frais Kilométrique',	0.62),
('NUI',	'Nuitée Hôtel',	80.00),
('REP',	'Repas Restaurant',	25.00);

INSERT INTO `LigneFraisForfait` (`idVisiteur`, `mois`, `idFraisForfait`, `quantite`) VALUES
('a131',	'01',	'ETP',	0),
('a131',	'01',	'KM',	0),
('a131',	'01',	'NUI',	0),
('a131',	'01',	'REP',	0);

DROP TABLE IF EXISTS `LigneFraisHorsForfait`;
CREATE TABLE `LigneFraisHorsForfait` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `idVisiteur` char(4) NOT NULL,
  `mois` char(6) NOT NULL,
  `libelle` varchar(100) DEFAULT NULL,
  `date` date DEFAULT NULL,
  `montant` decimal(10,2) DEFAULT NULL,
  `modePaiement` char(1) DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `idVisiteur` (`idVisiteur`,`mois`),
  KEY `modePaiement` (`modePaiement`),
  CONSTRAINT `LigneFraisHorsForfait_ibfk_1` FOREIGN KEY (`idVisiteur`, `mois`) REFERENCES `FicheFrais` (`idVisiteur`, `mois`),
  CONSTRAINT `LigneFraisHorsForfait_ibfk_2` FOREIGN KEY (`modePaiement`) REFERENCES `ModePaiement` (`code`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

INSERT INTO `LigneFraisHorsForfait` (`id`, `idVisiteur`, `mois`, `libelle`, `date`, `montant`, `modePaiement`) VALUES
(4,	'a131',	'01',	'Saisie clôturées',	'2023-03-30',	100.00,	NULL),
(5,	'a131',	'01',	'Saisie clôturées',	'2023-03-30',	100.00,	NULL),
(6,	'a131',	'01',	'Saisie clôturées',	'2023-03-30',	100.00,	NULL),
(7,	'a131',	'01',	'Saisie clôturées',	'2023-03-30',	100.00,	NULL);

INSERT INTO `ModePaiement` (`code`, `libelle`) VALUES
('1',	'Espèces'),
('2',	'Chèque'),
('3',	'Carte Bancaire');