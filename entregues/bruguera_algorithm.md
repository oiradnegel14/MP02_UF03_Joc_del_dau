# Burnout

A partir del resultat del rival adopta una postura segons el resultat del rival sempre que els punts 
siguin inferior a 3 sino se'ls atribueix a ell mateix

```
CREATE FUNCTION daus(@jugador as int, @punts as int)
RETURNS bit
AS BEGIN
	DECLARE @quedo as bit, @resultat as int, @resultatrival as int
	SET @resultat = (SELECT SUM(m.puntsAnotats)
			FROM Marcador m
			WHERE nJugadorAnota=@jugador)
	SET @resultatrival = (SELECT SUM(m.puntsAnotats)
				FROM Marcador m
				WHERE nJugadorAnota!=@jugador)
	IF (@punts>3)
		BEGIN
			SET @quedo =1
		END
	ELSE
		BEGIN
			IF (@resultatrival-2>@resultat)
				BEGIN
					SET @quedo =1
				END
			ELSE
				BEGIN
					SET @quedo =0
				END
		END
	RETURN @quedo
END
```
