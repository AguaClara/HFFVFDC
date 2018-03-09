```python
from aide_design.play import*
from aide_design.physchem import*
Q_Plant=20*u.L/u.s
Temp_Plant=20*u.degC
RatioVCOrifice=.62
Nu=viscosity_kinematic(Temp_Plant)
print(Nu)
Max_Num_Holes=19
Q_Per_Hole=Q_Plant/Max_Num_Holes
print(Q_Per_Hole)
#Rows_Per_T_Active_Area= 1 or 2
#Active_Height_Of_T=.13*u.m
#Min/Max_Orifices_Per_Row=
Avail_Head_High_Est=2*u.m
Avail_Head_Low_Est=1*u.m

Outlet_Diam=2*u.inch
Area_Outlet=((Outlet_Diam/2)**2)*u.pi/4
Slider_Pipe_ID=1.5*u.inch
SliderPipeLength=.405*u.m
Slider_Hole_Diam=.25*u.inch
Area_Slider_Hole=(((Slider_Hole_ID/2)**2)*u.pi/4)
print(Area_Slider_Hole.to(u.m**2))
V_Outlet=Q_Plant/((Outlet_Diam/2)**2)*u.pi/4
print(V_Outlet.to(u.m/u.s))

V_Hole=(Q_Per_Hole/Area_Slider_Hole)
print(V_Hole.to(u.m/u.s))
Reynolds=re_pipe(Q_Per_Hole, Slider_Hole_Diam, Nu)
print(Reynolds)
tee_height=5.25*u.inch  
bushing_lip=.21875*u.inch   
bushing_height=1*u.inch   
tee_exposed=tee_height-2*bushing_height*bushing_lip
top_space=1.75*u.inch
bottom_space=bushing_height+tee_exposed+Slider_Hole_Diam/2
L_active=overall_length-top_space-bottom_space
hole_rows=7
rows_exposed=3
row_spacing=tee_exposed/rows_exposed

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

```

Range_Slider is not for sure...
Check if this commits and pushes
