```python
from aide_design.play import*
from aide_design.physchem import*
Q_Plant=20*u.L/u.s
Avail_Head_High_Est=2*u.m
Avail_Head_Low_Est=1*u.m

OutletDiam=8*u.inch
FVDiam=6*u.inch
SliderPipeLength=.762*u.m
Slider_Pipe_Hole_Diam=.5*u.inch
Range_Slider=1.2*u.m
Z_Top_Hole=1.343*u.m
Z_Bot_Hole=.368*u.m


def K_Minor_Calc(D1,D2):
  K_L=(1-D1**2/D2**2)**2
  return(K_L)

  ##From left to right D1->D2
K_Minor_Inlet=K_Minor_Calc(OutletDiam,FVDiam) ##K minor value for first contraction
print(K_Minor_Inlet)
K_Minor_Slider_Holes=K_Minor_Calc(FVDiam,SliderPipeLength) ##K minor value for sliderp ipe holes
print(K_Minor_Slider_Holes)

HL_Inlet=headloss_exp(Q_Plant, OutletDiam, K_Minor_Inlet)
print(HL_Inlet)

HL_Slider_Pipe=headloss_exp(Q_Plant, Slider_Pipe_Hole_Diam, K_Minor_Slider_Holes)
print(HL_Slider_Pipe)

```
Range_Slider is not for sure...
