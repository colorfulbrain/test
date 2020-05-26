% volread.m for matlab
% based on spm

gmtemp=spm_vol('$PATH/HOA112_1mm.nii');                              % read nii
wmtemp=spm_vol('$PATH/rICBM_DTI_81_WMPM_60p_FMRIB58.nii');

gmdata=spm_read_vols(gmtemp);                                        % read each voxel
wmdata=spm_read_vols(wmtemp);

data=gmdata+wmdata;                                                  % combine GM and WM
data_onlycerebral=data;
data_onlycerebral(data_onlycerebral~=0)=1;                           % set all value~=0 as 1

tem2=gmtemp                                                          % write nii
tem2.fname='cerebral.nii';
tem2.private.dat.fname=tem2.fname;

spm_write_vol(tem2,data_onlycerebral);
