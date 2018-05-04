# hola
Aquesta funcio retorna TRUE si la puntuacio de la tirada és més gran que 3, i sino retorna FALSE.

```
create function dbo.mElsQuedo(@numeroJugador int,@puntuacioTirada int)
returns bit
as begin
	declare @bit as bit
	declare @puntsRival as int
		set @puntsRival = (select puntsAnotats from marcador where nJugadorAnota!=@numeroJugador)
	declare @puntsMeus as int 
		set @puntsMeus = (select puntsAnotats from marcador where nJugadorAnota=@numeroJugador)

	if @puntsRival>@puntsMeus or @puntuacioTirada>3
		begin
			set @bit=1
		end
	else
		begin
			set @bit=0
		end
	return @bit
end
```
