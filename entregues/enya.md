# AhoraSiQueSix3

DadosDaditos
La funció retorna, depenent dels punts, un bit per si el jugador s'els queda o els dona a l'oponent, controlant la suma dels punts de tots dos.

```

go
create function dbo.mElsQuedo(@nJugador int, @punts int)
 returns bit
 as begin
	declare @peraqui as bit
	declare @mispuntos int
	declare @puntoscontrario int
	set @mispuntos = (select sum(puntsAnotats)
						from Marcador
						where @nJugador = nJugadorAnota)
	set @puntoscontrario = (select sum(puntsAnotats)
						from Marcador
						where @nJugador != nJugadorAnota)
	declare @puntosconsuma int
	set @puntosconsuma = @mispuntos + @punts
	if(@puntosconsuma >= @puntoscontrario)
	begin
		set @peraqui = 1;
	end
	else
	begin
		set @peraqui = 0;
	end
	return @peraqui
end

```
