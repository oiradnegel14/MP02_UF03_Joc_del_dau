# Quedarse la tirada de dado
Mi funcion hace que si la diferencia de puntos en una tirada es mas grande o igual que 2 se lo quede
```
create function dbo.mElsQuedo(
  @nJugador as int,
  @punts as int
)returns bit
as begin
declare @guardarlo as bit, @misPuntos as int , @losDelOtro as int;
  set @misPuntos=(select Sum(m.puntsAnotats)from marcador m where @nJugador=nJugadorAnota)
  set @losDelOtro=(select sum(m.puntsAnotats)from marcador m where @nJugador!=nJugadorAnota)
    if (@punts>=3)begin
        if((@misPuntos-@losDelOtro)>2)begin
          set @guardarlo=1;
        end else begin
          set  @guardarlo=0;
        end
    end else begin
        if (@misPuntos-@losDelOtro)>2begin 
          set @guardarlo=1;
        end else begin
          set @guardarlo=0;
        end
    end
    return @guardarlo;
end;
```
