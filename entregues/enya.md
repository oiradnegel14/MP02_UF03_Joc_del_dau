# AhoraSiQueSix2

DadosDaditos
La funcio, retorna, depenent dels punts, un bit, per si el jugador s'els queda o el dona al oponent.

```

go
create function dbo.mElsQuedo(@nJugador int, @punts int)
 returns bit
 as begin
	declare @peraqui as bit
	declare @mipuntos int
	declare @puntoscontrario int
	set @mipuntos = (select sum(puntsAnotats)
						from Marcador
						where @nJugador = nJugadorAnota)
	set @puntoscontrario = (select sum(puntsAnotats)
						from Marcador
						where @nJugador != nJugadorAnota)
	if(@mipuntos+@punts >@puntoscontrario)
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
