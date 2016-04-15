# ROC_Gabor
% ROC_Analyzer: will conduct analysis of compare_PatchGabors_lite_modified
% processed files and return ROC statistics for different features.
close all
clear all
sessionfile = 'm16150309_001_rMGHP';
ecimg= 'p120';
filepath = ['C:\DATA\Kiwi\Processed Files\m16\MGHP\figures\ROC Figures\' ecimg '\'];
load(['C:\DATA\Kiwi\Processed Files\m16\MGHP\Gabor Analysis\bwscenes\patchstats_degraded_2by2\' sessionfile '.mat'])
addpath(genpath('C:/DATA/Kiwi/Processed Files/m16/MGHP/'));
Nboot=100;
%Compute then Graph Salience (Ss,Sc) ROC
a = Ss;
a(a==0)=NaN;
b = Sc;
b(b==0)=NaN;
[S_AUC, S_false, S_true, S_xmesh] = do_ROC_stats(a(~isnan(a)), b(~isnan(b)));
[S_bootstat, bootsam] = bootstrp(Nboot, @(z) bootstrp(1, @(p) do_ROC_stats(p,z), a), b);
Sv_CI = prctile(S_bootstat, [2.5 50 97.5]);
f1=figure
plot(cumsum(flipdim(S_false,1)), cumsum(flipdim(S_true,1)),'k-', 'LineWidth', 2); hold on;
plot([0,1], [0,1], 'k--');
title('Salience');
axis([0 1 0 1]);
%subplot(2,maxfeat,maxfeat+1); hold on;
f2=figure
plot(S_xmesh, S_true/sum(S_true), 'k', S_xmesh, S_false/sum(S_false), 'k--');
title('Salience');

%Compute then Graph Relevance (Rs,Rc) ROC
a = Rs;
a(a==0)=NaN;
b = Rc;
b(b==0)=NaN;
[R_AUC, R_false, R_true, R_xmesh] = do_ROC_stats(a(~isnan(a)), b(~isnan(b)));
[R_bootstat, bootsam] = bootstrp(Nboot, @(z) bootstrp(1, @(p) do_ROC_stats(p,z), a), b);
Rh_CI = prctile(R_bootstat, [2.5 50 97.5]);
f3=figure
plot(cumsum(flipdim(R_false,1)), cumsum(flipdim(R_true,1)),'k-', 'LineWidth', 2); hold on;
plot([0,1], [0,1], 'k--');
title('Relevance');
axis([0 1 0 1]);
%subplot(2,maxfeat,maxfeat+1); hold on;
f4=figure
plot(R_xmesh, R_true/sum(R_true), 'k', R_xmesh, R_false/sum(R_false), 'k--');
title('Relevance');

%Compute then Graph Energy (EN_s,EN_c) ROC
a = EN_s;
a(a==0)=NaN;
b = EN_c;
b(b==0)=NaN;
[EN_AUC, EN_false, EN_true, EN_xmesh] = do_ROC_stats(a(~isnan(a)), b(~isnan(b)));
[EN_bootstat, bootsam] = bootstrp(Nboot, @(z) bootstrp(1, @(p) do_ROC_stats(p,z), a), b);
EN_h_CI = prctile(EN_bootstat, [2.5 50 97.5]);
f5=figure
plot(cumsum(flipdim(EN_false,1)), cumsum(flipdim(EN_true,1)),'k-', 'LineWidth', 2); hold on;
plot([0,1], [0,1], 'k--');
title('Energy');
axis([0 1 0 1]);
%subplot(2,maxfeat,maxfeat+1); hold on;
f6=figure
plot(EN_xmesh, EN_true/sum(EN_true), 'k', EN_xmesh, EN_false/sum(EN_false), 'k--');
title('Energy');

%Compute then Graph Orientedness (ORNESS_s,ORNESS_c) ROC
a = ORNESS_s;
a(a==0)=NaN;
b = ORNESS_c;
b(b==0)=NaN;
[ORNESS_AUC, ORNESS_false, ORNESS_true, ORNESS_xmesh] = do_ROC_stats(a(~isnan(a)), b(~isnan(b)));
[ORNESS_bootstat, bootsam] = bootstrp(Nboot, @(z) bootstrp(1, @(p) do_ROC_stats(p,z), a), b);
ORNESS_v_CI = prctile(ORNESS_bootstat, [2.5 50 97.5]);
f7=figure
plot(cumsum(flipdim(ORNESS_false,1)), cumsum(flipdim(ORNESS_true,1)),'k-', 'LineWidth', 2); hold on;
plot([0,1], [0,1], 'k--');
title('Orientedness');
axis([0 1 0 1]);
%subplot(2,maxfeat,maxfeat+1); hold on;
f8=figure
plot(ORNESS_xmesh, ORNESS_true/sum(ORNESS_true), 'k', ORNESS_xmesh, ORNESS_false/sum(ORNESS_false), 'k--');
title('Orientedness');

%Compute then Graph Orientation-sine (ORI_s,ORI_c) ROC
a = ORI_s;
a(a==0)=NaN;
b = ORI_c;
b(b==0)=NaN;
[ORI_AUC, ORI_false, ORI_true, ORI_xmesh] = do_ROC_stats(abs(sin(a(~isnan(a)))), abs(sin(b(~isnan(b)))));
[ORI_bootstat, bootsam] = bootstrp(Nboot, @(z) bootstrp(1, @(p) do_ROC_stats(p,z), abs(sin(a))), abs(sin(b)));
ORI_v_CI = prctile(ORI_bootstat, [2.5 50 97.5]);
f9=figure
plot(cumsum(flipdim(ORI_false,1)), cumsum(flipdim(ORI_true,1)),'k-', 'LineWidth', 2); hold on;
plot([0,1], [0,1], 'k--');
title('Orientation (Sine)');
axis([0 1 0 1]);
%subplot(2,maxfeat,maxfeat+1); hold on;
f10=figure
plot(ORI_xmesh, ORI_true/sum(ORI_true), 'k', ORI_xmesh, ORI_false/sum(ORI_false), 'k--');
title('Orientation (Sine)');

%Compute then Graph Orientation-cosine (ORI_s,ORI_c) ROC
a = ORI_s;
a(a==0)=NaN;
b = ORI_c;
b(b==0)=NaN;
[ORI_AUC, ORI_false, ORI_true, ORI_xmesh] = do_ROC_stats(abs(cos(a(~isnan(a)))), abs(cos(b(~isnan(b)))));
[ORI_bootstat, bootsam] = bootstrp(Nboot, @(z) bootstrp(1, @(p) do_ROC_stats(p,z), abs(cos(a))), abs(cos(b)));
ORI_v_CI = prctile(ORI_bootstat, [2.5 50 97.5]);
f11=figure
plot(cumsum(flipdim(ORI_false,1)), cumsum(flipdim(ORI_true,1)),'k-', 'LineWidth', 2); hold on;
plot([0,1], [0,1], 'k--');
title('Orientation (Cosine)');
axis([0 1 0 1]);
%subplot(2,maxfeat,maxfeat+1); hold on;
f12=figure
plot(ORI_xmesh, ORI_true/sum(ORI_true), 'k', ORI_xmesh, ORI_false/sum(ORI_false), 'k--');
title('Orientation (Cosine)');

save(['C:/DATA/Kiwi/Processed Files/m16/MGHP/Gabor Analysis/bwscenes/Processed_Patchstats/' ecimg '/' sessionfile])
saveas(f1 ,[filepath sessionfile ', salience1'],'jpeg')
saveas(f2,[filepath sessionfile ', salience2'],'jpeg')
saveas(f3,[filepath sessionfile ', relevance1'],'jpeg')
saveas(f4,[filepath sessionfile ', relevance2'],'jpeg')
saveas(f5,[filepath sessionfile ', energy1'],'jpeg')
saveas(f6,[filepath sessionfile ', energy2'],'jpeg')
saveas(f7,[filepath  sessionfile ', orientedness1'],'jpeg')
saveas(f8,[filepath sessionfile ', orientedness2'],'jpeg')
saveas(f9,[filepath sessionfile ', sinorientation1'],'jpeg')
saveas(f10,[filepath sessionfile ', sineorientation2'],'jpeg')
saveas(f11,[filepath sessionfile ', cosorientation1'],'jpeg')
saveas(f12,[filepath sessionfile ', cosorientation2'],'jpeg')
