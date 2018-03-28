```python
from aide_design.play import*
from aide_design.physchem import*
import math
Q_Plant=20*u.L/u.s
Temp_Plant=20*u.degC
RatioVCOrifice=.62
Nu=viscosity_kinematic(Temp_Plant)
print(Nu)
Max_Num_Holes=10
Q_Per_Hole=Q_Plant/Max_Num_Holes
print(Q_Per_Hole)
#Rows_Per_T_Active_Area= 1 or 2
#Active_Height_Of_T=.13*u.m
#Min/Max_Orifices_Per_Row=
Avail_Head_High_Est=2*u.m
Avail_Head_Low_Est=1*u.m

FS_Diam=8*u.inch
Area_Outlet=((FS_Diam/2)**2)*u.pi/4
#SS_Diam=4*u.inch     SS - Small scale
FS_FV_Diam=6*u.inch
#SS_FV_Diam=3*u.inch     SS- Small Scale
SliderPipeLength=.762*u.m
Slider_Hole_Diam=1*u.inch
Area_Slider_Hole=(((Slider_Hole_Diam/2)**2)*u.pi/4)
print(Area_Slider_Hole.to(u.m**2))
V_Outlet=Q_Plant/((FS_Diam/2)**2)*u.pi/4
print(V_Outlet.to(u.m/u.s))

V_Hole=(Q_Per_Hole/Area_Slider_Hole)
print(V_Hole.to(u.m/u.s))
Reynolds=re_pipe(Q_Per_Hole, Slider_Hole_Diam, Nu)
print(Reynolds)
Range_Slider=1.2*u.m
Z_Top_Hole=1.343*u.m
Z_Bot_Hole=.368*u.m
Range_Slider=1.2*u.m ## needs to be updated
Z_Top_Hole=1.343*u.m ## and here
Z_Bot_Hole=.368*u.m ## same here

def K_Minor_Calc(D1,D2):
  K_L=(1-D1**2/D2**2)**2
  return(K_L)
K_Minor_Calc(8*u.inch,6*u.inch)
  ##From left to right D1->D2,
K_Minor_Inlet=K_Minor_Calc(FS_Diam,FS_FV_Diam)
 ##K minor value for first contraction
print(K_Minor_Inlet)

HL_Inlet=headloss_exp(Q_Plant, FS_FV_Diam, K_Minor_Inlet)
print(HL_Inlet)

HL_Slider_Hole=head_orifice(Slider_Hole_Diam, RatioVCOrifice, Q_Per_Hole)
print(HL_Slider_Hole)


flow_orifice_1= flow_orifice(Slider_Hole_Diam, 1*u.m, RatioVCOrifice)
print(flow_orifice_1*Max_Num_Holes)
flow_orifice_2= flow_orifice(Slider_Hole_Diam, 2*u.m, RatioVCOrifice)
print(flow_orifice_2.to(u.L/u.s))

#Function to solve for slider hole diameter
def Slider_Diam(FlowRate,Headloss_Avail):
  Diameter=((4*FlowRate)/(math.pi*(2*u.gravity*Headloss_Avail)**.5))**.5
  return(Diameter)
  
# Functino to solve for Float length
def Float_Length(r, fricForce, temp):
  floatLength = (fricForce/u.gravity)/(density_water(temp) * math.pi * r**2 * (.5))
  return floatLength.to(u.m)
Float_Length(.5*u.inch, 17.67*u.N, Temp_Plant)


  ##The the float was designed in relation to the frictional force so that when the float is in the plant, it will sit half submerged in the water.
```

Range_Slider is not for sure...
Check if this commits and pushes
