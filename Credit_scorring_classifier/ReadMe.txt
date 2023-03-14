Heatmap:
'Accent', 'Accent_r', 'Blues', 'Blues_r', 'BrBG', 'BrBG_r', 'BuGn', 'BuGn_r', 'BuPu', 'BuPu_r', 'CMRmap', 'CMRmap_r', 'Dark2', 'Dark2_r', 'GnBu', 'GnBu_r', 'Greens', 'Greens_r', 'Greys', 'Greys_r', 'OrRd', 'OrRd_r', 'Oranges', 'Oranges_r', 'PRGn', 'PRGn_r', 'Paired', 'Paired_r', 'Pastel1', 'Pastel1_r', 'Pastel2', 'Pastel2_r', 'PiYG', 'PiYG_r', 'PuBu', 'PuBuGn', 'PuBuGn_r', 'PuBu_r', 'PuOr', 'PuOr_r', 'PuRd', 'PuRd_r', 'Purples', 'Purples_r', 'RdBu', 'RdBu_r', 'RdGy', 'RdGy_r', 'RdPu', 'RdPu_r', 'RdYlBu', 'RdYlBu_r', 'RdYlGn', 'RdYlGn_r', 'Reds', 'Reds_r', 'Set1', 'Set1_r', 'Set2', 'Set2_r', 'Set3', 'Set3_r', 'Spectral', 'Spectral_r', 'Wistia', 'Wistia_r', 'YlGn', 'YlGnBu', 'YlGnBu_r', 'YlGn_r', 'YlOrBr', 'YlOrBr_r', 'YlOrRd', 'YlOrRd_r', 'afmhot', 'afmhot_r', 'autumn', 'autumn_r', 'binary', 'binary_r', 'bone', 'bone_r', 'brg', 'brg_r', 'bwr', 'bwr_r', 'cividis', 'cividis_r', 'cool', 'cool_r', 'coolwarm', 'coolwarm_r', 'copper', 'copper_r', 'crest', 'crest_r', 'cubehelix', 'cubehelix_r', 'flag', 'flag_r', 'flare', 'flare_r', 'gist_earth', 'gist_earth_r', 'gist_gray', 'gist_gray_r', 'gist_heat', 'gist_heat_r', 'gist_ncar', 'gist_ncar_r', 'gist_rainbow', 'gist_rainbow_r', 'gist_stern', 'gist_stern_r', 'gist_yarg', 'gist_yarg_r', 'gnuplot', 'gnuplot2', 'gnuplot2_r', 'gnuplot_r', 'gray', 'gray_r', 'hot', 'hot_r', 'hsv', 'hsv_r', 'icefire', 'icefire_r', 'inferno', 'inferno_r', 'jet', 'jet_r', 'magma', 'magma_r', 'mako', 'mako_r', 'nipy_spectral', 'nipy_spectral_r', 'ocean', 'ocean_r', 'pink', 'pink_r', 'plasma', 'plasma_r', 'prism', 'prism_r', 'rainbow', 'rainbow_r', 'rocket', 'rocket_r', 'seismic', 'seismic_r', 'spring', 'spring_r', 'summer', 'summer_r', 'tab10', 'tab10_r', 'tab20', 'tab20_r', 'tab20b', 'tab20b_r', 'tab20c', 'tab20c_r', 'terrain', 'terrain_r', 'turbo', 'turbo_r', 'twilight', 'twilight_r', 'twilight_shifted', 'twilight_shifted_r', 'viridis', 'viridis_r', 'vlag', 'vlag_r', 'winter', 'winter_r'

**Описание датасета**

* **Home Ownership** - домовладение
* **Annual Income** - годовой доход
* **Years in current job** - количество лет на текущем месте работы
* **Tax Liens** - налоговые обременения
* **Number of Open Accounts** - количество открытых счетов
* **Years of Credit History** - количество лет кредитной истории
* **Maximum Open Credit** - наибольший открытый кредит
* **Number of Credit Problems** - количество проблем с кредитом
* **Months since last delinquent** - количество месяцев с последней просрочки платежа
* **Bankruptcies** - банкротства
* **Purpose** - цель кредита
* **Term** - срок кредита
* **Current Loan Amount** - текущая сумма кредита
* **Current Credit Balance** - текущий кредитный баланс
* **Monthly Debt** - ежемесячный долг
* **Credit Score** - кредитный рейтинг
* **Credit Default** - факт невыполнения кредитных обязательств (0 - погашен вовремя, 1 - просрочка)

'Категориальные признаки: cat_list, 
[+'Home Ownership',
 -'Years in current job',
 +/-'Purpose',
 +'Term',
 -'Tax Liens',
 +'Number of Credit Problems',
 -'Bankruptcies']

'Непрерывные и порядковые признаки: ' num_list, 
[+'Annual Income',
 'Number of Open Accounts',+
 'Years of Credit History',+
 'Maximum Open Credit',
 -'Months since last delinquent',
 +'Current Loan Amount',
 'Current Credit Balance',+
 'Monthly Debt',+
 ++'Credit Score']

'Целевой признак: 'target_name
'Credit Default'

Для пайплайна: 
class OutliersDetection():
    """собирает статистики числовых признаков и заменяет выбросные значения на медианные"""
    
    def __init__(self, qq_threshhold_min, qq_threshhold_max, numeric_features):
        """Параметры класса-список статистик, определяющих условия удаления выбросов"""
        self.threshhold_min = qq_threshhold_min #нижний перцентиль для удаления выбросов
        self.threshhold_max = qq_threshhold_max #верхний перцентиль для удаления выбросов
        self.features_to_transform = numeric_features # список признаков, в которых нужно обработать быбросы
        self.feature_stats = None #для сохранения статистик по каждому вещественному признаку
        
        
методы: fit, transform

class MyImputer():
    """Заменит пропуски"""
    def __init__(self, cat_features, num_features, corr_features):
        """Параметры класса"""
        self.cat_strategy = 'most_frequent'
        self.num_strategy = 'median'
        self.cat_features_to_impute = cat_features #список категориальных признаков для замены пропусков
        self.num_features_to_impute = num_features #список количественных признаков для замены пропусков
        self.corr_features_to_impute = corr_features #список коррелирующих признаков для замены пропусков (первым в списке должен стоять заполняемый признак!)
        self.stats_to_impute = None #для сохранения статистик для заполнения пропусков (получаются в методе fit)

методы: fit, transform

 cclass CatFeaturesTransformer():
    """Приводит категориальные данные в нужный формат, укрупняет категории"""
    
    def __init__(self, features_to_transform, features_to_dummi):
        """Параметры класса, содержат списки для замены значений категорий"""
        self.years_to_replace = ['<3 лет стажа', '3-8 лет стажа', '> 8 лет стажа']
        self.purpose_to_replace = ['debt consolidation', 'other']
        self.features_for_decrese_cats = features_to_transform # список признаков, которые нужно обработать
        self.features_get_dummies = features_to_dummi #список признаков для преобразования в дамми=переменные 

методы: fit_transform 

class CorrFeaturesTransformer():
    """Преобразуем коррелирующие между собой признаки в один, понизив размерность данные методом PCA"""
    def __init__(self, features_corr):
                 """Параметры класса, содержат подмножества признаков для объединения в одну размерность"""
            self.features_to_transform = features_corr #кортеж из списков преобразуемых признаков 
    
методы: fit_transform 
cclass BadFeaturesTransformer():
    """удалит плохие признаки"""
    
    def __init__(self, features_to_delete_list):
                 """Параметры класса, содержат списки для замены значений категорий"""
            self.features_to_delete = features_to_delete_list #список удаляемых признаков
            self.bad_features_deleted = None #список удаленных признаков
       


