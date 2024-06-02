<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Agent Immobilier - Omnes Immobilier</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header>
        <h1>Agent Immobilier</h1>
    </header>
    <nav>
        <ul>
            <li><a href="index.html">Accueil</a></li>
            <li><a href="browse.php">Tout Parcourir</a></li>
            <li><a href="search.php">Recherche</a></li>
            <li><a href="appointments.php">Rendez-vous</a></li>
            <li><a href="account.php">Votre Compte</a></li>
        </ul>
    </nav>
    <main>
        <?php
        include 'config.php';

        if (isset($_GET['id'])) {
            $agent_id = intval($_GET['id']);
            $sql = "SELECT * FROM agents WHERE id=$agent_id";
            $result = $conn->query($sql);

            if ($result->num_rows > 0) {
                $row = $result->fetch_assoc();
                echo '<div class="agent-detail">';
                echo '<div class="agent-photo"><img src="' . $row["photo"] . '" alt="Agent Photo"></div>';
                echo '<div class="agent-info">';
                echo '<h2>' . $row["bio"] . '</h2>';
                echo '<p>Email : ' . $row["email"] . '</p>';
                echo '<p>Téléphone : ' . $row["phone"] . '</p>';
                echo '</div>';
                echo '</div>';
                echo '<div class="agent-actions">';
                echo '<a href="mailto:' . $row["email"] . '" class="contact-button">Contacter par mail</a>';
                echo '<a href="cv.php?id=' . $agent_id . '" class="contact-button">Voir son CV</a>';
                echo '<a href="appointment.php?agent_id=' . $agent_id . '" class="contact-button">Prendre un RDV</a>';
                echo '</div>';
            } else {
                echo '<p>Agent non trouvé.</p>';
            }
        } else {
            echo '<p>ID d\'agent non spécifié.</p>';
        }

        $conn->close();
        ?>
    </main>
    <footer>
        <p>Contactez-nous : <a href="mailto:info@omnesimmobilier.com">info@omnesimmobilier.com</a></p>
        <p>Adresse : 16 Rue Sextius Michel, Paris</p>
    </footer>
</body>
</html>
