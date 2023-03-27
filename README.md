# IMisc2
IMisc2: Identifing the disease associated clones, classifing two groups using these clones, and evaluating it performance by cross-validation from two group's (control && case) immune repertoire data.

Version: V2.0.0

1. Usage:
perl IMisc.pl   -id -ic -o -R [parameters]

            -id      <S> input clone files of disease samples' list
            -ic      <S> input clone files of control samples' list
            -o      <S> out directory


            -cd     <I> cutoff of Disease clone's supporting samples for FDR correction [2]
            -cc     <I> cutoff of Control clone's supporting samples for FDR correction [2]
            -ps     <S> pvalues for classification [1e-20:1e-15:1e-14:1e-13:1e-12:1e-11:1e-10:1e-9:1e-8:1e-7:1e-6:1e-5:1e-4:5e-4:1e-3:5e-3:1e-2:5e-2:1e-1:5e-1:1]
            -m      <I> mulitple shell for crossvidation, -m means how many smaples would be put together in a shell [10]
            -mode   <S> classification mode. RandomForest or Logistics [RandomForest]
            -topn   <I> use top N clone for final classification [3000]

            -R      <S> directory of Rscript [.../bin/R/R-3.4.1/bin/Rscript]

Note
           
The format of -id/-ic: two columns: <path of clone files> <sample name>. e.g. /home/zw/S1_CDR3_AA.frequency.clones.gz S1
        <path of clone files>: three columns, <clone> <reads_num> <frequency>. e.g. CASRNRGGNTEAFF_TRBV19_TRBJ1-1   10050   1.07618


2. After running the IMisc.pl program, *.sh would be generated, then running the *.sh as follows:

        1)sh Step1_identify_specific_clones.sh
        2)sh Crossvalidation_shell/Total_crossvalidation.sh or sh Crossvalidation_shell/step1*.sh and then sh step2.sh
                this step is to do the leave-one-out cross-validation, and would require long time. If you don't need the result of this, just skip it and run the next *.sh
        3)sh Step3_calculate_memburden_allsamples.sh
        4)sh Step4.figure.sh
