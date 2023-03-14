Heatmap:
'Accent', 'Accent_r', 'Blues', 'Blues_r', 'BrBG', 'BrBG_r', 'BuGn', 'BuGn_r', 'BuPu', 'BuPu_r', 'CMRmap', 'CMRmap_r', 'Dark2', 'Dark2_r', 'GnBu', 'GnBu_r', 'Greens', 'Greens_r', 'Greys', 'Greys_r', 'OrRd', 'OrRd_r', 'Oranges', 'Oranges_r', 'PRGn', 'PRGn_r', 'Paired', 'Paired_r', 'Pastel1', 'Pastel1_r', 'Pastel2', 'Pastel2_r', 'PiYG', 'PiYG_r', 'PuBu', 'PuBuGn', 'PuBuGn_r', 'PuBu_r', 'PuOr', 'PuOr_r', 'PuRd', 'PuRd_r', 'Purples', 'Purples_r', 'RdBu', 'RdBu_r', 'RdGy', 'RdGy_r', 'RdPu', 'RdPu_r', 'RdYlBu', 'RdYlBu_r', 'RdYlGn', 'RdYlGn_r', 'Reds', 'Reds_r', 'Set1', 'Set1_r', 'Set2', 'Set2_r', 'Set3', 'Set3_r', 'Spectral', 'Spectral_r', 'Wistia', 'Wistia_r', 'YlGn', 'YlGnBu', 'YlGnBu_r', 'YlGn_r', 'YlOrBr', 'YlOrBr_r', 'YlOrRd', 'YlOrRd_r', 'afmhot', 'afmhot_r', 'autumn', 'autumn_r', 'binary', 'binary_r', 'bone', 'bone_r', 'brg', 'brg_r', 'bwr', 'bwr_r', 'cividis', 'cividis_r', 'cool', 'cool_r', 'coolwarm', 'coolwarm_r', 'copper', 'copper_r', 'crest', 'crest_r', 'cubehelix', 'cubehelix_r', 'flag', 'flag_r', 'flare', 'flare_r', 'gist_earth', 'gist_earth_r', 'gist_gray', 'gist_gray_r', 'gist_heat', 'gist_heat_r', 'gist_ncar', 'gist_ncar_r', 'gist_rainbow', 'gist_rainbow_r', 'gist_stern', 'gist_stern_r', 'gist_yarg', 'gist_yarg_r', 'gnuplot', 'gnuplot2', 'gnuplot2_r', 'gnuplot_r', 'gray', 'gray_r', 'hot', 'hot_r', 'hsv', 'hsv_r', 'icefire', 'icefire_r', 'inferno', 'inferno_r', 'jet', 'jet_r', 'magma', 'magma_r', 'mako', 'mako_r', 'nipy_spectral', 'nipy_spectral_r', 'ocean', 'ocean_r', 'pink', 'pink_r', 'plasma', 'plasma_r', 'prism', 'prism_r', 'rainbow', 'rainbow_r', 'rocket', 'rocket_r', 'seismic', 'seismic_r', 'spring', 'spring_r', 'summer', 'summer_r', 'tab10', 'tab10_r', 'tab20', 'tab20_r', 'tab20b', 'tab20b_r', 'tab20c', 'tab20c_r', 'terrain', 'terrain_r', 'turbo', 'turbo_r', 'twilight', 'twilight_r', 'twilight_shifted', 'twilight_shifted_r', 'viridis', 'viridis_r', 'vlag', 'vlag_r', 'winter', 'winter_r'

**�������� ��������**

* **Home Ownership** - ������������
* **Annual Income** - ������� �����
* **Years in current job** - ���������� ��� �� ������� ����� ������
* **Tax Liens** - ��������� �����������
* **Number of Open Accounts** - ���������� �������� ������
* **Years of Credit History** - ���������� ��� ��������� �������
* **Maximum Open Credit** - ���������� �������� ������
* **Number of Credit Problems** - ���������� ������� � ��������
* **Months since last delinquent** - ���������� ������� � ��������� ��������� �������
* **Bankruptcies** - �����������
* **Purpose** - ���� �������
* **Term** - ���� �������
* **Current Loan Amount** - ������� ����� �������
* **Current Credit Balance** - ������� ��������� ������
* **Monthly Debt** - ����������� ����
* **Credit Score** - ��������� �������
* **Credit Default** - ���� ������������ ��������� ������������ (0 - ������� �������, 1 - ���������)

'�������������� ��������: cat_list, 
[+'Home Ownership',
 -'Years in current job',
 +/-'Purpose',
 +'Term',
 -'Tax Liens',
 +'Number of Credit Problems',
 -'Bankruptcies']

'����������� � ���������� ��������: ' num_list, 
[+'Annual Income',
 'Number of Open Accounts',+
 'Years of Credit History',+
 'Maximum Open Credit',
 -'Months since last delinquent',
 +'Current Loan Amount',
 'Current Credit Balance',+
 'Monthly Debt',+
 ++'Credit Score']

'������� �������: 'target_name
'Credit Default'

��� ���������: 
class OutliersDetection():
    """�������� ���������� �������� ��������� � �������� ��������� �������� �� ���������"""
    
    def __init__(self, qq_threshhold_min, qq_threshhold_max, numeric_features):
        """��������� ������-������ ���������, ������������ ������� �������� ��������"""
        self.threshhold_min = qq_threshhold_min #������ ���������� ��� �������� ��������
        self.threshhold_max = qq_threshhold_max #������� ���������� ��� �������� ��������
        self.features_to_transform = numeric_features # ������ ���������, � ������� ����� ���������� �������
        self.feature_stats = None #��� ���������� ��������� �� ������� ������������� ��������
        
        
������: fit, transform

class MyImputer():
    """������� ��������"""
    def __init__(self, cat_features, num_features, corr_features):
        """��������� ������"""
        self.cat_strategy = 'most_frequent'
        self.num_strategy = 'median'
        self.cat_features_to_impute = cat_features #������ �������������� ��������� ��� ������ ���������
        self.num_features_to_impute = num_features #������ �������������� ��������� ��� ������ ���������
        self.corr_features_to_impute = corr_features #������ ������������� ��������� ��� ������ ��������� (������ � ������ ������ ������ ����������� �������!)
        self.stats_to_impute = None #��� ���������� ��������� ��� ���������� ��������� (���������� � ������ fit)

������: fit, transform

 cclass CatFeaturesTransformer():
    """�������� �������������� ������ � ������ ������, ��������� ���������"""
    
    def __init__(self, features_to_transform, features_to_dummi):
        """��������� ������, �������� ������ ��� ������ �������� ���������"""
        self.years_to_replace = ['<3 ��� �����', '3-8 ��� �����', '> 8 ��� �����']
        self.purpose_to_replace = ['debt consolidation', 'other']
        self.features_for_decrese_cats = features_to_transform # ������ ���������, ������� ����� ����������
        self.features_get_dummies = features_to_dummi #������ ��������� ��� �������������� � �����=���������� 

������: fit_transform 

class CorrFeaturesTransformer():
    """����������� ������������� ����� ����� �������� � ����, ������� ����������� ������ ������� PCA"""
    def __init__(self, features_corr):
                 """��������� ������, �������� ������������ ��������� ��� ����������� � ���� �����������"""
            self.features_to_transform = features_corr #������ �� ������� ������������� ��������� 
    
������: fit_transform 
cclass BadFeaturesTransformer():
    """������ ������ ��������"""
    
    def __init__(self, features_to_delete_list):
                 """��������� ������, �������� ������ ��� ������ �������� ���������"""
            self.features_to_delete = features_to_delete_list #������ ��������� ���������
            self.bad_features_deleted = None #������ ��������� ���������
       


