# Joc del Dau
## Funció mElsQuedo

- La meva funció recull els punts totals dels dos jugadors.
- En el primer if comprova si l'altre jugador te més punts que actual, si es així i la tirada dels daus es igual o més gran que 4 se la queda.
- En el segon if comprova si el jugador actual té més punts que l'altre o si son iguals, si es així se la queda.
- I finalment un else que deixara sempre amb 0 quan no siguin aquests dos casos.

```
create function mElsQuedo (
@nJugador int,
@punts int) returns bit
as begin
	declare @bit bit, @punts_altre_jugador int, @punts_jugador int;
	set @punts_jugador = 
		(select sum(puntsanotats) from Marcador where nJugadorAnota = @nJugador )+@punts;
	set @punts_altre_jugador = 
		(select sum(puntsanotats) from Marcador where nJugadorAnota != @nJugador );
	if(@punts_altre_jugador > @punts_jugador and @punts >= 4)
		begin
			set @bit = 1;
		end
	if(@punts_jugador > @punts_altre_jugador or @punts_jugador = @punts_altre_jugador)
		begin
			set @bit = 1;
		end
	else
		begin
			set @bit = 0;
		end
return @bit;
end
```
