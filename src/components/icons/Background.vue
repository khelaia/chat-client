<template>
    <div class="background">
        <svg xmlns="http://www.w3.org/2000/svg" version="1.1" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:svgjs="http://svgjs.dev/svgjs" width="1440" height="560" preserveAspectRatio="none" viewBox="0 0 1440 560">
            <g mask="url(&quot;#SvgjsMask1000&quot;)" fill="none">
                <rect width="1440" height="560" x="0" y="0" fill="#0e2a47"></rect>
                <path d="M727.9160559283082 236.78800985379291L824.4796439074029 218.01794977096915 805.7095838245791 121.45436179187442 709.1459958454844 140.22442187469818z" fill="rgba(28, 83, 142, 0.4)" class="triangle-float3"></path>
                <path d="M615.4280593388593 102.56282534070758L717.4891534940987 77.21942496588866 654.7951471983807 9.98833430827031z" fill="rgba(28, 83, 142, 0.4)" class="triangle-float2"></path>
                <path d="M1093.439,193.001C1112.433,193.281,1130.71,184.202,1140.243,167.771C1149.808,151.284,1149.081,130.622,1139.022,114.431C1129.48,99.072,1111.51,91.81,1093.439,92.434C1076.47,93.02,1061.747,102.848,1053,117.401C1043.947,132.463,1040.678,150.929,1048.967,166.424C1057.697,182.745,1074.932,192.728,1093.439,193.001" fill="rgba(28, 83, 142, 0.4)" class="triangle-float2"></path>
                <path d="M523.2871033077232 218.06938041112917L376.49426319721243 186.86759903946174 345.292481825545 333.6604391499725 492.0853219360558 364.86222052164z" fill="rgba(28, 83, 142, 0.4)" class="triangle-float2"></path>
                <path d="M1156.092327140698 202.0597136283444L1241.061050417475 179.29241284442853 1218.293749633559 94.32368956765167 1133.325026356782 117.09099035156756z" fill="rgba(28, 83, 142, 0.4)" class="triangle-float1"></path>
                <path d="M103.919,531.617C134.416,532.843,167.019,521.481,180.726,494.21C193.566,468.662,176.857,440.756,161.806,416.445C147.866,393.93,130.399,370.394,103.919,370.152C77.15,369.908,57.338,392.062,44.173,415.371C31.275,438.206,25.122,465.112,37.11,488.438C50.101,513.715,75.522,530.476,103.919,531.617" fill="rgba(28, 83, 142, 0.4)" class="triangle-float2"></path>
            </g>
            <defs>
                <mask id="SvgjsMask1000">
                    <rect width="1440" height="560" fill="#ffffff"></rect>
                </mask>
                
            </defs>
        </svg>
    </div>
</template>

<style>
    @keyframes float1 {
            0%{transform: translate(0, 0)}
            50%{transform: translate(-10px, 0)}
            100%{transform: translate(0, 0)}
        }

        .triangle-float1 {
            animation: float1 5s infinite;
        }

        @keyframes float2 {
            0%{transform: translate(0, 0)}
            50%{transform: translate(-5px, -5px)}
            100%{transform: translate(0, 0)}
        }

        .triangle-float2 {
            animation: float2 4s infinite;
        }

        @keyframes float3 {
            0%{transform: translate(0, 0)}
            50%{transform: translate(0, -10px)}
            100%{transform: translate(0, 0)}
        }

        .triangle-float3 {
            animation: float3 6s infinite;
        }
</style>