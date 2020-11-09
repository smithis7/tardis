.. code:: ipython3

    import ads
    import pandas as pd
    ads.config.token="" 

.. code:: ipython3

    papers = ads.SearchQuery(q='(((full:"tardis" AND (full:"kerzendorf" OR (bibstem:"Natur" AND full:"supernova")))) AND year:2014-)+property:refereed', sort="date",
                             fl = ['bibcode','title', 'bibstem', 'author', 'year'])
    
    bibcodes = []
    titles = []
    bibstems = []
    authors = []
    year_list = []
    for paper in papers:
        bibcodes.append(paper.bibcode)
        titles.append(paper.title)
        bibstems.append(paper.bibstem)
        authors.append(paper.author)
        year_list.append(paper.year)

.. code:: ipython3

    def get_url(bibcodes):
        """This function takes the list of bibcodes and returns a link!"""
        url_list = []
        for bibcode in bibcodes:
            url = "https://ui.adsabs.harvard.edu/abs/{}".format(bibcode)
            url_list.append(url)
        return url_list

.. code:: ipython3

    def get_journal(bibstems):
        """This function takes the list of bibstems and returns the journal that they are in, formatted."""
        journals = []
        for item in bibstems:
            journals.append(item[0])
        return journals

.. code:: ipython3

    def get_authors_formatted(authors):
        """This gets the first 3 authors of each paper. If there are more than 3, the first 3 followed by 'et al.
        is returned. If it's less than or equal to 3, the first 3 are returned. This function takes in a list and 
        returns a modified version of the list"""
        formatted_author_list=[]
        for author_array in authors: #Note that array is just being used as a variable, no array is used
            count=0
            author_string = ""
            for item in author_array:
                if count==0:
                    author_string+=item
                    count+=1
                elif count<3:
                    author_string+=", "+item
                    count+=1
                elif count==3:
                    author_string+=", et al."
                    break
            formatted_author_list.append(author_string)
        return formatted_author_list

.. code:: ipython3

    def get_titles_formatted(titles):
        formatted_titles_list = []
        for title in titles:
            title_str = ""
            for item in title:
                title_str += str(item)
            formatted_titles_list.append(title_str)
        return formatted_titles_list

.. code:: ipython3

    d = {'Authors': get_authors_formatted(authors), 'Year': year_list, 'Journal': get_journal(bibstems), 
         'Title': get_titles_formatted(titles), 'Link': get_url(bibcodes)}
    df = pd.DataFrame(data=d)
    df.to_csv('adslist.csv')

.. code:: ipython3

    string_list='' #This is not a list btw. This is a string of strings. 
    
    for i in range(len(list(year_list))):
        string_list+= "    " + get_authors_formatted(authors)[i]+' '+year_list[i]+', '+get_journal(bibstems)[i]+',\
        "'+get_titles_formatted(titles)[i]+'" '+get_url(bibcodes)[i]+"""
        
        
    """

.. code:: ipython3

    print(string_list)


.. parsed-literal::

        Magee, M. R., Maguire, K. 2020, A&A,    "An investigation of <SUP>56</SUP>Ni shells as the source of early light curve bumps in type Ia supernovae" https://ui.adsabs.harvard.edu/abs/2020A&A...642A.189M
        
        
        Chen, Xingzhuo, Hu, Lei, Wang, Lifan 2020, ApJS,    "Artificial Intelligence-Assisted Inversion (AIAI) of Synthetic Type Ia Supernova Spectra" https://ui.adsabs.harvard.edu/abs/2020ApJS..250...12C
        
        
        Miller, A. A., Magee, M. R., Polin, A., et al. 2020, ApJ,    "The Spectacular Ultraviolet Flash from the Peculiar Type Ia Supernova 2019yvq" https://ui.adsabs.harvard.edu/abs/2020ApJ...898...56M
        
        
        Gillanders, J. H., Sim, S. A., Smartt, S. J. 2020, MNRAS,    "AT2018kzr: the merger of an oxygen-neon white dwarf and a neutron star or black hole" https://ui.adsabs.harvard.edu/abs/2020MNRAS.497..246G
        
        
        Bouquin, Daina R., Chivvis, Daniel A., Henneken, Edwin, et al. 2020, ApJS,    "Credit Lost: Two Decades of Software Citation in Astronomy" https://ui.adsabs.harvard.edu/abs/2020ApJS..249....8B
        
        
        Tomasella, Lina, Stritzinger, Maximilian, Benetti, Stefano, et al. 2020, MNRAS,    "Observations of the low-luminosity Type Iax supernova 2019gsc: a fainter clone of SN 2008ha?" https://ui.adsabs.harvard.edu/abs/2020MNRAS.496.1132T
        
        
        Livneh, Ran, Katz, Boaz 2020, MNRAS,    "An asymmetric explosion mechanism may explain the diversity of Si II linewidths in Type Ia supernovae" https://ui.adsabs.harvard.edu/abs/2020MNRAS.494.5811L
        
        
        Kawabata, Miho, Maeda, Keiichi, Yamanaka, Masayuki, et al. 2020, ApJ,    "SN 2019ein: New Insights into the Similarities and Diversity among High-velocity Type Ia Supernovae" https://ui.adsabs.harvard.edu/abs/2020ApJ...893..143K
        
        
        Srivastav, Shubham, Smartt, Stephen J., Leloudas, Giorgos, et al. 2020, ApJL,    "The Lowest of the Low: Discovery of SN 2019gsc and the Nature of Faint Iax Supernovae" https://ui.adsabs.harvard.edu/abs/2020ApJ...892L..24S
        
        
        Magee, M. R., Maguire, K., Kotak, R., et al. 2020, A&A,    "Determining the <SUP>56</SUP>Ni distribution of type Ia supernovae from observations within days of explosion" https://ui.adsabs.harvard.edu/abs/2020A&A...634A..37M
        
        
        Vogl, C., Kerzendorf, W. E., Sim, S. A., et al. 2020, A&A,    "Spectral modeling of type II supernovae. II. A machine-learning approach to quantitative spectroscopic analysis" https://ui.adsabs.harvard.edu/abs/2020A&A...633A..88V
        
        
        McBrien, Owen R., Smartt, Stephen J., Chen, Ting-Wan, et al. 2019, ApJL,    "SN2018kzr: A Rapidly Declining Transient from the Destruction of a White Dwarf" https://ui.adsabs.harvard.edu/abs/2019ApJ...885L..23M
        
        
        Watson, Darach, Hansen, Camilla J., Selsing, Jonatan, et al. 2019, Natur,    "Identification of strontium in the merger of two neutron stars" https://ui.adsabs.harvard.edu/abs/2019Natur.574..497W
        
        
        Jacobson-Galán, Wynn V., Foley, Ryan J., Schwab, Josiah, et al. 2019, MNRAS,    "Detection of circumstellar helium in Type Iax progenitor systems" https://ui.adsabs.harvard.edu/abs/2019MNRAS.487.2538J
        
        
        Noebauer, Ulrich M., Sim, Stuart A. 2019, LRCA,    "Monte Carlo radiative transfer" https://ui.adsabs.harvard.edu/abs/2019LRCA....5....1N
        
        
        Chatzopoulos, E., Weide, K. 2019, ApJ,    "Gray Radiation Hydrodynamics with the FLASH Code for Astrophysical Applications" https://ui.adsabs.harvard.edu/abs/2019ApJ...876..148C
        
        
        Mulligan, Brian W., Zhang, Kaicheng, Wheeler, J. Craig 2019, MNRAS,    "Exploring the shell model of high-velocity features of Type Ia supernovae using TARDIS" https://ui.adsabs.harvard.edu/abs/2019MNRAS.484.4785M
        
        
        Magee, M. R., Sim, S. A., Kotak, R., et al. 2019, A&A,    "Detecting the signatures of helium in type Iax supernovae" https://ui.adsabs.harvard.edu/abs/2019A&A...622A.102M
        
        
        Heringer, E., van Kerkwijk, M. H., Sim, S. A., et al. 2019, ApJ,    "Spectral Sequences of Type Ia Supernovae. II. Carbon as a Diagnostic Tool for Explosion Mechanisms" https://ui.adsabs.harvard.edu/abs/2019ApJ...871..250H
        
        
        Izzo, L., de Ugarte Postigo, A., Maeda, K., et al. 2019, Natur,    "Signatures of a jet cocoon in early spectra of a supernova associated with a γ-ray burst" https://ui.adsabs.harvard.edu/abs/2019Natur.565..324I
        
        
        Vogl, C., Sim, S. A., Noebauer, U. M., et al. 2019, A&A,    "Spectral modeling of type II supernovae. I. Dilution factors" https://ui.adsabs.harvard.edu/abs/2019A&A...621A..29V
        
        
        Ergon, M., Fransson, C., Jerkstrand, A., et al. 2018, A&A,    "Monte-Carlo methods for NLTE spectral synthesis of supernovae" https://ui.adsabs.harvard.edu/abs/2018A&A...620A.156E
        
        
        Barna, Barnabás, Szalai, Tamás, Kerzendorf, Wolfgang E., et al. 2018, MNRAS,    "Type Iax supernovae as a few-parameter family" https://ui.adsabs.harvard.edu/abs/2018MNRAS.480.3609B
        
        
        Prentice, S. J., Maguire, K., Smartt, S. J., et al. 2018, ApJL,    "The Cow: Discovery of a Luminous, Hot, and Rapidly Evolving Transient" https://ui.adsabs.harvard.edu/abs/2018ApJ...865L...3P
        
        
        Beaujean, Frederik, Eggers, Hans C., Kerzendorf, Wolfgang E. 2018, MNRAS,    "Bayesian modelling of uncertainties of Monte Carlo radiative-transfer simulations" https://ui.adsabs.harvard.edu/abs/2018MNRAS.477.3425B
        
        
        Magee, M. R., Sim, S. A., Kotak, R., et al. 2018, A&A,    "Modelling the early time behaviour of type Ia supernovae: effects of the <SUP>56</SUP>Ni distribution" https://ui.adsabs.harvard.edu/abs/2018A&A...614A.115M
        
        
        Röpke, Friedrich K., Sim, Stuart A. 2018, SSRv,    "Models for Type Ia Supernovae and Related Astrophysical Transients" https://ui.adsabs.harvard.edu/abs/2018SSRv..214...72R
        
        
        Barna, Barnabás, Szalai, Tamás, Kromer, Markus, et al. 2017, MNRAS,    "Abundance tomography of Type Iax SN 2011ay with tardis" https://ui.adsabs.harvard.edu/abs/2017MNRAS.471.4865B
        
        
        Smartt, S. J., Chen, T. -W., Jerkstrand, A., et al. 2017, Natur,    "A kilonova as the electromagnetic counterpart to a gravitational-wave source" https://ui.adsabs.harvard.edu/abs/2017Natur.551...75S
        
        
        Heringer, E., van Kerkwijk, M. H., Sim, S. A., et al. 2017, ApJ,    "Spectral Sequences of Type Ia Supernovae. I. Connecting Normal and Subluminous SNe Ia and the Presence of Unburned Carbon" https://ui.adsabs.harvard.edu/abs/2017ApJ...846...15H
        
        
        Magee, M. R., Kotak, R., Sim, S. A., et al. 2017, A&A,    "Growing evidence that SNe Iax are not a one-parameter family. The case of PS1-12bwh" https://ui.adsabs.harvard.edu/abs/2017A&A...601A..62M
        
        
        Boyle, Aoife, Sim, Stuart A., Hachinger, Stephan, et al. 2017, A&A,    "Helium in double-detonation models of type Ia supernovae" https://ui.adsabs.harvard.edu/abs/2017A&A...599A..46B
        
        
        Noebauer, U. M., Taubenberger, S., Blinnikov, S., et al. 2016, MNRAS,    "Type Ia supernovae within dense carbon- and oxygen-rich envelopes: a model for `Super-Chandrasekhar' explosions?" https://ui.adsabs.harvard.edu/abs/2016MNRAS.463.2972N
        
        
        Inserra, C., Bulla, M., Sim, S. A., et al. 2016, ApJ,    "Spectropolarimetry of Superluminous Supernovae: Insight into Their Geometry" https://ui.adsabs.harvard.edu/abs/2016ApJ...831...79I
        
        
        Szalai, Tamás, Vinkó, József, Nagy, Andrea P., et al. 2016, MNRAS,    "The continuing story of SN IIb 2013df: new optical and IR observations and analysis" https://ui.adsabs.harvard.edu/abs/2016MNRAS.460.1500S
        
        
        Magee, M. R., Kotak, R., Sim, S. A., et al. 2016, A&A,    "The type Iax supernova, SN 2015H. A white dwarf deflagration candidate" https://ui.adsabs.harvard.edu/abs/2016A&A...589A..89M
        
        
        Dubernet, M. L., Antony, B. K., Ba, Y. A., et al. 2016, JPhB,    "The virtual atomic and molecular data centre (VAMDC) consortium" https://ui.adsabs.harvard.edu/abs/2016JPhB...49g4003D
        
        
        Parrent, J. T., Howell, D. A., Fesen, R. A., et al. 2016, MNRAS,    "Comparative analysis of SN 2012dn optical spectra: days -14 to +114" https://ui.adsabs.harvard.edu/abs/2016MNRAS.457.3702P
        
        
        Young, P. R., Dere, K. P., Landi, E., et al. 2016, JPhB,    "The CHIANTI atomic database" https://ui.adsabs.harvard.edu/abs/2016JPhB...49g4009Y
        
        
        Noebauer, U. M., Sim, S. A. 2015, MNRAS,    "Self-consistent modelling of line-driven hot-star winds with Monte Carlo radiation hydrodynamics" https://ui.adsabs.harvard.edu/abs/2015MNRAS.453.3120N
        
        
        Matthews, J. H., Knigge, C., Long, K. S., et al. 2015, MNRAS,    "The impact of accretion disc winds on the optical spectra of cataclysmic variables" https://ui.adsabs.harvard.edu/abs/2015MNRAS.450.3331M
        
        
        Kerzendorf, Wolfgang E., Sim, Stuart A. 2014, MNRAS,    "A spectral synthesis code for rapid modelling of supernovae" https://ui.adsabs.harvard.edu/abs/2014MNRAS.440..387K
        
        
    


.. code:: ipython3

    df




.. raw:: html

    <div>
    <style scoped>
        .dataframe tbody tr th:only-of-type {
            vertical-align: middle;
        }
    
        .dataframe tbody tr th {
            vertical-align: top;
        }
    
        .dataframe thead th {
            text-align: right;
        }
    </style>
    <table border="1" class="dataframe">
      <thead>
        <tr style="text-align: right;">
          <th></th>
          <th>Authors</th>
          <th>Year</th>
          <th>Journal</th>
          <th>Title</th>
          <th>Link</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>0</th>
          <td>Magee, M. R., Maguire, K.</td>
          <td>2020</td>
          <td>A&amp;A</td>
          <td>An investigation of &lt;SUP&gt;56&lt;/SUP&gt;Ni shells as ...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2020A&amp;A...64...</td>
        </tr>
        <tr>
          <th>1</th>
          <td>Chen, Xingzhuo, Hu, Lei, Wang, Lifan</td>
          <td>2020</td>
          <td>ApJS</td>
          <td>Artificial Intelligence-Assisted Inversion (AI...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2020ApJS..25...</td>
        </tr>
        <tr>
          <th>2</th>
          <td>Miller, A. A., Magee, M. R., Polin, A., et al.</td>
          <td>2020</td>
          <td>ApJ</td>
          <td>The Spectacular Ultraviolet Flash from the Pec...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2020ApJ...89...</td>
        </tr>
        <tr>
          <th>3</th>
          <td>Gillanders, J. H., Sim, S. A., Smartt, S. J.</td>
          <td>2020</td>
          <td>MNRAS</td>
          <td>AT2018kzr: the merger of an oxygen-neon white ...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2020MNRAS.49...</td>
        </tr>
        <tr>
          <th>4</th>
          <td>Bouquin, Daina R., Chivvis, Daniel A., Henneke...</td>
          <td>2020</td>
          <td>ApJS</td>
          <td>Credit Lost: Two Decades of Software Citation ...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2020ApJS..24...</td>
        </tr>
        <tr>
          <th>5</th>
          <td>Tomasella, Lina, Stritzinger, Maximilian, Bene...</td>
          <td>2020</td>
          <td>MNRAS</td>
          <td>Observations of the low-luminosity Type Iax su...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2020MNRAS.49...</td>
        </tr>
        <tr>
          <th>6</th>
          <td>Livneh, Ran, Katz, Boaz</td>
          <td>2020</td>
          <td>MNRAS</td>
          <td>An asymmetric explosion mechanism may explain ...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2020MNRAS.49...</td>
        </tr>
        <tr>
          <th>7</th>
          <td>Kawabata, Miho, Maeda, Keiichi, Yamanaka, Masa...</td>
          <td>2020</td>
          <td>ApJ</td>
          <td>SN 2019ein: New Insights into the Similarities...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2020ApJ...89...</td>
        </tr>
        <tr>
          <th>8</th>
          <td>Srivastav, Shubham, Smartt, Stephen J., Leloud...</td>
          <td>2020</td>
          <td>ApJL</td>
          <td>The Lowest of the Low: Discovery of SN 2019gsc...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2020ApJ...89...</td>
        </tr>
        <tr>
          <th>9</th>
          <td>Magee, M. R., Maguire, K., Kotak, R., et al.</td>
          <td>2020</td>
          <td>A&amp;A</td>
          <td>Determining the &lt;SUP&gt;56&lt;/SUP&gt;Ni distribution o...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2020A&amp;A...63...</td>
        </tr>
        <tr>
          <th>10</th>
          <td>Vogl, C., Kerzendorf, W. E., Sim, S. A., et al.</td>
          <td>2020</td>
          <td>A&amp;A</td>
          <td>Spectral modeling of type II supernovae. II. A...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2020A&amp;A...63...</td>
        </tr>
        <tr>
          <th>11</th>
          <td>McBrien, Owen R., Smartt, Stephen J., Chen, Ti...</td>
          <td>2019</td>
          <td>ApJL</td>
          <td>SN2018kzr: A Rapidly Declining Transient from ...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2019ApJ...88...</td>
        </tr>
        <tr>
          <th>12</th>
          <td>Watson, Darach, Hansen, Camilla J., Selsing, J...</td>
          <td>2019</td>
          <td>Natur</td>
          <td>Identification of strontium in the merger of t...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2019Natur.57...</td>
        </tr>
        <tr>
          <th>13</th>
          <td>Jacobson-Galán, Wynn V., Foley, Ryan J., Schwa...</td>
          <td>2019</td>
          <td>MNRAS</td>
          <td>Detection of circumstellar helium in Type Iax ...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2019MNRAS.48...</td>
        </tr>
        <tr>
          <th>14</th>
          <td>Noebauer, Ulrich M., Sim, Stuart A.</td>
          <td>2019</td>
          <td>LRCA</td>
          <td>Monte Carlo radiative transfer</td>
          <td>https://ui.adsabs.harvard.edu/abs/2019LRCA.......</td>
        </tr>
        <tr>
          <th>15</th>
          <td>Chatzopoulos, E., Weide, K.</td>
          <td>2019</td>
          <td>ApJ</td>
          <td>Gray Radiation Hydrodynamics with the FLASH Co...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2019ApJ...87...</td>
        </tr>
        <tr>
          <th>16</th>
          <td>Mulligan, Brian W., Zhang, Kaicheng, Wheeler, ...</td>
          <td>2019</td>
          <td>MNRAS</td>
          <td>Exploring the shell model of high-velocity fea...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2019MNRAS.48...</td>
        </tr>
        <tr>
          <th>17</th>
          <td>Magee, M. R., Sim, S. A., Kotak, R., et al.</td>
          <td>2019</td>
          <td>A&amp;A</td>
          <td>Detecting the signatures of helium in type Iax...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2019A&amp;A...62...</td>
        </tr>
        <tr>
          <th>18</th>
          <td>Heringer, E., van Kerkwijk, M. H., Sim, S. A.,...</td>
          <td>2019</td>
          <td>ApJ</td>
          <td>Spectral Sequences of Type Ia Supernovae. II. ...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2019ApJ...87...</td>
        </tr>
        <tr>
          <th>19</th>
          <td>Izzo, L., de Ugarte Postigo, A., Maeda, K., et...</td>
          <td>2019</td>
          <td>Natur</td>
          <td>Signatures of a jet cocoon in early spectra of...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2019Natur.56...</td>
        </tr>
        <tr>
          <th>20</th>
          <td>Vogl, C., Sim, S. A., Noebauer, U. M., et al.</td>
          <td>2019</td>
          <td>A&amp;A</td>
          <td>Spectral modeling of type II supernovae. I. Di...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2019A&amp;A...62...</td>
        </tr>
        <tr>
          <th>21</th>
          <td>Ergon, M., Fransson, C., Jerkstrand, A., et al.</td>
          <td>2018</td>
          <td>A&amp;A</td>
          <td>Monte-Carlo methods for NLTE spectral synthesi...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2018A&amp;A...62...</td>
        </tr>
        <tr>
          <th>22</th>
          <td>Barna, Barnabás, Szalai, Tamás, Kerzendorf, Wo...</td>
          <td>2018</td>
          <td>MNRAS</td>
          <td>Type Iax supernovae as a few-parameter family</td>
          <td>https://ui.adsabs.harvard.edu/abs/2018MNRAS.48...</td>
        </tr>
        <tr>
          <th>23</th>
          <td>Prentice, S. J., Maguire, K., Smartt, S. J., e...</td>
          <td>2018</td>
          <td>ApJL</td>
          <td>The Cow: Discovery of a Luminous, Hot, and Rap...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2018ApJ...86...</td>
        </tr>
        <tr>
          <th>24</th>
          <td>Beaujean, Frederik, Eggers, Hans C., Kerzendor...</td>
          <td>2018</td>
          <td>MNRAS</td>
          <td>Bayesian modelling of uncertainties of Monte C...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2018MNRAS.47...</td>
        </tr>
        <tr>
          <th>25</th>
          <td>Magee, M. R., Sim, S. A., Kotak, R., et al.</td>
          <td>2018</td>
          <td>A&amp;A</td>
          <td>Modelling the early time behaviour of type Ia ...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2018A&amp;A...61...</td>
        </tr>
        <tr>
          <th>26</th>
          <td>Röpke, Friedrich K., Sim, Stuart A.</td>
          <td>2018</td>
          <td>SSRv</td>
          <td>Models for Type Ia Supernovae and Related Astr...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2018SSRv..21...</td>
        </tr>
        <tr>
          <th>27</th>
          <td>Barna, Barnabás, Szalai, Tamás, Kromer, Markus...</td>
          <td>2017</td>
          <td>MNRAS</td>
          <td>Abundance tomography of Type Iax SN 2011ay wit...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2017MNRAS.47...</td>
        </tr>
        <tr>
          <th>28</th>
          <td>Smartt, S. J., Chen, T. -W., Jerkstrand, A., e...</td>
          <td>2017</td>
          <td>Natur</td>
          <td>A kilonova as the electromagnetic counterpart ...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2017Natur.55...</td>
        </tr>
        <tr>
          <th>29</th>
          <td>Heringer, E., van Kerkwijk, M. H., Sim, S. A.,...</td>
          <td>2017</td>
          <td>ApJ</td>
          <td>Spectral Sequences of Type Ia Supernovae. I. C...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2017ApJ...84...</td>
        </tr>
        <tr>
          <th>30</th>
          <td>Magee, M. R., Kotak, R., Sim, S. A., et al.</td>
          <td>2017</td>
          <td>A&amp;A</td>
          <td>Growing evidence that SNe Iax are not a one-pa...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2017A&amp;A...60...</td>
        </tr>
        <tr>
          <th>31</th>
          <td>Boyle, Aoife, Sim, Stuart A., Hachinger, Steph...</td>
          <td>2017</td>
          <td>A&amp;A</td>
          <td>Helium in double-detonation models of type Ia ...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2017A&amp;A...59...</td>
        </tr>
        <tr>
          <th>32</th>
          <td>Noebauer, U. M., Taubenberger, S., Blinnikov, ...</td>
          <td>2016</td>
          <td>MNRAS</td>
          <td>Type Ia supernovae within dense carbon- and ox...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2016MNRAS.46...</td>
        </tr>
        <tr>
          <th>33</th>
          <td>Inserra, C., Bulla, M., Sim, S. A., et al.</td>
          <td>2016</td>
          <td>ApJ</td>
          <td>Spectropolarimetry of Superluminous Supernovae...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2016ApJ...83...</td>
        </tr>
        <tr>
          <th>34</th>
          <td>Szalai, Tamás, Vinkó, József, Nagy, Andrea P.,...</td>
          <td>2016</td>
          <td>MNRAS</td>
          <td>The continuing story of SN IIb 2013df: new opt...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2016MNRAS.46...</td>
        </tr>
        <tr>
          <th>35</th>
          <td>Magee, M. R., Kotak, R., Sim, S. A., et al.</td>
          <td>2016</td>
          <td>A&amp;A</td>
          <td>The type Iax supernova, SN 2015H. A white dwar...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2016A&amp;A...58...</td>
        </tr>
        <tr>
          <th>36</th>
          <td>Dubernet, M. L., Antony, B. K., Ba, Y. A., et al.</td>
          <td>2016</td>
          <td>JPhB</td>
          <td>The virtual atomic and molecular data centre (...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2016JPhB...4...</td>
        </tr>
        <tr>
          <th>37</th>
          <td>Parrent, J. T., Howell, D. A., Fesen, R. A., e...</td>
          <td>2016</td>
          <td>MNRAS</td>
          <td>Comparative analysis of SN 2012dn optical spec...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2016MNRAS.45...</td>
        </tr>
        <tr>
          <th>38</th>
          <td>Young, P. R., Dere, K. P., Landi, E., et al.</td>
          <td>2016</td>
          <td>JPhB</td>
          <td>The CHIANTI atomic database</td>
          <td>https://ui.adsabs.harvard.edu/abs/2016JPhB...4...</td>
        </tr>
        <tr>
          <th>39</th>
          <td>Noebauer, U. M., Sim, S. A.</td>
          <td>2015</td>
          <td>MNRAS</td>
          <td>Self-consistent modelling of line-driven hot-s...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2015MNRAS.45...</td>
        </tr>
        <tr>
          <th>40</th>
          <td>Matthews, J. H., Knigge, C., Long, K. S., et al.</td>
          <td>2015</td>
          <td>MNRAS</td>
          <td>The impact of accretion disc winds on the opti...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2015MNRAS.45...</td>
        </tr>
        <tr>
          <th>41</th>
          <td>Kerzendorf, Wolfgang E., Sim, Stuart A.</td>
          <td>2014</td>
          <td>MNRAS</td>
          <td>A spectral synthesis code for rapid modelling ...</td>
          <td>https://ui.adsabs.harvard.edu/abs/2014MNRAS.44...</td>
        </tr>
      </tbody>
    </table>
    </div>



.. code:: ipython3

    sphinx-build . _build


::


    -------------

    NameErrorTraceback (most recent call last)

    <ipython-input-11-905b8097446d> in <module>
    ----> 1 sphinx-build . _build
    

    NameError: name 'sphinx' is not defined


