# Function-Sergi
Aquesta funció agafa la puntuació sempre que el nombre sigui major o igual a tres. Si el nombre es menor a tres només l'agafa si la puntuació del rival menys dos punts es superior a la puntuació del jugador.
```
CREATE FUNCTION dbo.Mels_quedo
(
	@N_jugador as int, @Punts as int
)
RETURNS bit
AS BEGIN
	DECLARE @Meus as bit, @Total as int, @Totalrival as int
	SET @Total = (SELECT SUM(puntsAnotats)
			FROM marcador M
			WHERE M.nJugadorAnota=@N_jugador)
	SET @Totalrival = (SELECT SUM(puntsAnotats)
			FROM marcador M
			WHERE M.nJugadorAnota!=@N_jugador)
	IF (@Punts>=3)
		BEGIN
			SET @Meus =1
		END
	ELSE
		BEGIN
			IF (@Punts<3 AND @Totalrival-2>@Total)
				BEGIN
					SET @Meus =1
				END
			ELSE
				BEGIN
					SET @Meus =0
				END
		END
	RETURN @Meus
END
```
